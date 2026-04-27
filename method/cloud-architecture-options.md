---
classification: confidential
owner: GrowDirect LLC
type: method-reference
nav_order: 5
---

# Cloud Architecture Options for CATz Deployments

Every CATz engagement runs somewhere. This article is the decision framework for where.

The CATz stack has specific infrastructure requirements that interact differently with each cloud platform's pricing, managed service availability, and operational posture. Getting this decision right during Scaffold is load-bearing: the wrong choice surfaces at scale, not at proof of concept.

---

## The CATz Stack — Infrastructure Requirements

The Canary Retail platform that anchors every CATz engagement depends on five infrastructure primitives:

| Requirement | Component | Notes |
|---|---|---|
| Relational database + vector index | PostgreSQL 17 + pgvector extension | pgvector must be available; version compatibility matters — not all managed PostgreSQL offerings run 17 at extension-compatible patch levels |
| In-memory data structure store | Valkey 8 (Redis-compatible) | Used for sessions, cache, Valkey Streams for the TSP ingestion pipeline. Managed offerings under the "Redis" label vary widely in compatibility |
| Local inference / embedding | Ollama with qwen3-embedding:8b | 1024-dimension vectors; GPU-accelerated preferred but CPU workloads are viable at SMB scale — matters for container sizing |
| Object storage | S3-compatible | Transaction exports, vault snapshots, tenant backups |
| Container runtime | Flask 3 + Gunicorn | Deployed in containers; managed container options vary in operational overhead |

---

## Platform Comparison

### PostgreSQL 17 + pgvector

The canonical choice for managed PostgreSQL is a function of whether pgvector is available and at what version cost. pgvector 0.7+ is required for 1024-dimension index support (half-vector compression and HNSW indexes).

| Platform | Managed Offering | pgvector Support | Cost Reference (us-east-1 / us-central-1 / eastus equivalent) |
|---|---|---|---|
| **AWS** | RDS for PostgreSQL, Aurora PostgreSQL | pgvector available on RDS PostgreSQL 15+, Aurora PostgreSQL 15+. AWS maintains pgvector actively — version support is current. | RDS db.t3.micro (1 vCPU, 1GB RAM): ~$14/month + $0.115/GB-month storage. db.t3.small (2 vCPU, 2GB RAM): ~$28/month. Multi-AZ doubles the compute cost. |
| **GCP** | Cloud SQL for PostgreSQL | pgvector available as an extension since Cloud SQL PostgreSQL 15. AlloyDB (Aurora equivalent) supports pgvector. | Cloud SQL db-g1-small (0.5 vCPU, 1.7GB RAM): ~$25/month + $0.17/GB-month SSD storage. Shared-core pricing attractive at low scale; jumps at growth. |
| **Azure** | Azure Database for PostgreSQL Flexible Server | pgvector supported on Flexible Server (PostgreSQL 13+). Extension enable/disable is self-service in Flexible Server. | Burstable B1ms (1 vCPU, 2GB RAM): ~$14/month + $0.115/GB-month storage. Comparable to AWS at entry tier. |

**Verdict.** AWS RDS PostgreSQL is the most operationally straightforward choice if the rest of the stack is AWS-native. Azure Flexible Server is price-competitive and the pgvector support is solid. GCP Cloud SQL is capable but the pricing model is less transparent at small scale.

---

### Valkey / Redis

Valkey is the Redis-compatible open-source fork. Managed offerings universally market themselves as "Redis compatible" — the critical check is Valkey Stream support, which drives the TSP ingestion pipeline.

| Platform | Managed Offering | Valkey/Redis Streams Support | Cost Reference |
|---|---|---|---|
| **AWS** | ElastiCache for Redis (OSS) | Streams supported. ElastiCache OSS Redis runs the upstream open-source codebase, not the Redis Ltd commercial version, making it Valkey-compatible. | cache.t3.micro (1 vCPU, 0.5GB): ~$13/month. cache.t3.small (1 vCPU, 1.4GB): ~$26/month. Multi-AZ: ~2x. |
| **GCP** | Memorystore for Redis (Cluster or Single Instance) | Streams supported in Memorystore for Redis 6.x+. | M1 Basic (1GB): ~$35/month. Higher floor than AWS/Azure at entry tier. |
| **Azure** | Azure Cache for Redis | Streams supported. C0 Basic (250MB) not suitable for Streams workloads; C1 Standard (1GB) is minimum viable. | C1 Standard: ~$54/month. Higher cost at entry tier; discounted substantially at reserved pricing (1-year: ~$33/month). |

**Verdict.** AWS ElastiCache is the lowest-cost entry and has the deepest operational tooling. For self-managed deployments (including GrowDirect-managed infrastructure where the retailer has control), Valkey can run in-container alongside the Flask app on a single EC2 instance — eliminating the managed service cost entirely until scale demands it.

---

### Ollama / GPU Inference (Embedding Workloads)

The `qwen3-embedding:8b` model running under Ollama generates 1024-dimension vectors for the memory bus. At SMB retailer scale (100–5,000 chunks/day being embedded), CPU-only inference is viable. GPU becomes relevant when embedding workloads exceed ~50,000 chunks/day — which corresponds roughly to a 100+ store rollout.

| Platform | GPU Option | Cost Reference (A10G-class or equivalent) | CPU Alternative |
|---|---|---|---|
| **AWS** | EC2 g4dn.xlarge (T4 GPU, 4 vCPU, 16GB RAM) | ~$0.526/hr on-demand; ~$0.188/hr Spot. For batch embedding jobs, Spot pricing is viable. ~$135/month sustained on-demand, ~$50/month as a Spot batch runner. | EC2 t3.medium (2 vCPU, 4GB RAM): ~$30/month. Viable for qwen3-embedding:8b at low throughput. |
| **GCP** | Cloud Run with GPU (NVIDIA L4, preview) | ~$0.80/hr for L4-attached Cloud Run jobs. Best for bursty, not sustained, workloads. | Cloud Run CPU: per-request billing eliminates idle cost. Suitable for low-frequency embedding jobs. |
| **Azure** | NC4as T4 v3 (T4 GPU, 4 vCPU, 28GB RAM) | ~$0.526/hr on-demand; reserved pricing competitive. | Standard_B2ms (2 vCPU, 8GB RAM): ~$60/month. More expensive CPU baseline than AWS. |

**Practical recommendation.** At SMB scale, run Ollama in a container on the application server (CPU-only). The embedding workload for a 5–15 store retailer is well within CPU capacity — qwen3-embedding:8b requires ~8GB RAM at full precision but runs acceptably on a 4GB instance with quantization. Separate GPU infrastructure only when the embedding queue consistently lags or when the retailer's vault is growing faster than ~10,000 new chunks/month.

---

### Object Storage

All three platforms offer S3-compatible object storage. The differentiating factor at CATz scale is egress cost and the cross-region transfer story when tenants are in one region and reporting consumers are in another.

| Platform | Offering | Storage Cost | Egress to Internet (per GB) |
|---|---|---|---|
| **AWS** | S3 Standard | $0.023/GB-month | $0.09/GB (first 10TB/month) |
| **GCP** | Cloud Storage Standard | $0.020/GB-month | $0.08/GB (Americas/Europe egress) |
| **Azure** | Blob Storage (LRS) | $0.018/GB-month | $0.087/GB |

At CATz scale (see [[method/data-economics]] for worked examples), storage differences are in the noise. Egress becomes the relevant cost when exporting transaction history to external analytics consumers or when migrating tenants. GCP is marginally cheaper on egress; AWS is the default because the rest of the stack already runs there.

---

### Managed Container Options

The CATz Flask stack runs in containers (Flask 3 + Gunicorn). Managed container platforms differ on cold-start latency, persistent volume support, and operational overhead for a workload that is persistent-process (not bursty/serverless).

| Platform | Offering | Fit for CATz Flask | Entry Cost |
|---|---|---|---|
| **AWS** | ECS Fargate, ECS on EC2 | Fargate is viable for the web tier; the TSP consumers (stream processors) run better on EC2 because they are persistent processes, not request-scoped. ECS on EC2 gives more control. | Fargate: ~$0.04048/vCPU-hour + $0.004445/GB-hour. For 0.5 vCPU / 1GB: ~$15/month. EC2 t3.micro: ~$7.50/month (bare instance). |
| **GCP** | Cloud Run | Cloud Run is request-scoped; persistent stream consumers require minimum instance = 1, which changes the cost profile. Not ideal for the TSP pipeline. Cloud Run Jobs work for batch workloads. | Cloud Run (0.5 vCPU / 512MB, always-on): ~$18/month. |
| **Azure** | Azure Container Apps | Similar to Cloud Run — consumption-based pricing favors bursty workloads. Persistent process model requires dedicated replicas. | Basic tier (0.5 vCPU / 1GB, dedicated): ~$13/month. |

**Verdict.** For small deployments (single tenant, low transaction volume), EC2 with Docker Compose is the simplest and cheapest option — no managed container service overhead. ECS on EC2 becomes attractive when operating 10+ tenants and the operational leverage of managed scheduling is worth the overhead.

---

## Recommended Posture

### Current Production (GrowDirect-Managed Infrastructure)

GrowDirect's production stack runs on EC2 t3.micro (AWS us-east-1) under the `growdirect.app` domain. This is the GrowDirect-managed posture: one EC2 instance runs the shared Docker Compose stack (PostgreSQL, Valkey, Ollama, Flask apps), with per-tenant database isolation on a single PostgreSQL host.

**This posture holds when:**
- Total tenant count ≤ 10 (connection pooling and shared PostgreSQL remain manageable)
- Aggregate transaction volume ≤ ~2,000 transactions/hour (EC2 t3.micro CPU stays below 70% sustained)
- No tenant has compliance requirements (PCI DSS, SOC 2) that demand dedicated infrastructure
- The VAR or MSP model (Rapid POS, for example) doesn't require tenant-specific cloud credentials

**When it breaks:**
- Any tenant requires dedicated cloud infrastructure (their own AWS account, their own RDS instance)
- Aggregate load exceeds t3.micro capacity — next tier is t3.small (~$15/month) or t3.medium (~$30/month)
- A third-party audit requires infrastructure isolation documentation that shared Docker Compose can't provide
- Sub-tenant MSP model: Rapid POS deploys Canary to their merchant base, and each merchant needs an isolated environment

### Upgrade Path at Scale

| Store Count | Tenant Model | Recommended Architecture | Estimated Monthly Infra Cost |
|---|---|---|---|
| 1–10 tenants, 1–50 stores total | Shared GrowDirect-managed | EC2 t3.small, shared PostgreSQL, Valkey, Ollama | ~$75–120/month shared |
| 10–50 tenants, 50–500 stores total | Hybrid: shared control plane, isolated data planes | EC2 t3.medium control plane; RDS t3.micro per tenant for databases; shared Valkey/Ollama | ~$50–75/month per tenant + ~$100/month shared infra |
| 50–200 tenants, 500–2,000 stores total | Fully isolated per tenant | ECS on EC2 per tenant, RDS per tenant, ElastiCache cluster shared or per-tenant | ~$80–150/month per tenant |
| 200+ tenants, 2,000+ stores | Platform play | Multi-region, auto-scaling, dedicated SRE discipline | ~$50–80/month per tenant at scale (unit economics improve) |

These are estimates. Actual costs vary materially based on transaction volume, data retention policy, and whether GPU inference is required.

---

## Tenant Isolation Model

The current production pattern is per-tenant PostgreSQL databases on a shared host. This is the lowest-cost isolation mechanism and the right starting posture for a GrowDirect-managed deployment.

### Per-Tenant Database Pattern (Current)

Each tenant gets:
- Dedicated PostgreSQL database (`canary_<tenant_id>`, `cove_<tenant_id>`)
- Database-level user with no cross-tenant privileges
- Valkey namespace isolation via key prefix convention (`<tenant_id>:*`)
- Application-layer tenant context enforcement (Flask middleware)

**Cost of 50 isolated tenant databases on each platform:**

| Platform | Service | Per-DB Cost | 50-tenant Total |
|---|---|---|---|
| **AWS RDS** | RDS t3.micro Multi-AZ shared cluster (Aurora Serverless v2) | Aurora Serverless v2: ~$0.12/ACU-hour; minimum 0.5 ACU. 50 databases on one Aurora instance: ~$43/month + $0.10/GB storage. | ~$100–200/month for 50 tenants (storage + ACU, light workload) |
| **AWS RDS** | RDS for PostgreSQL t3.micro per tenant (isolated instances) | ~$14/month/tenant × 50 = $700/month | $700/month — rarely the right choice at this scale |
| **GCP Cloud SQL** | Shared instance, per-database isolation | Cloud SQL is instance-scoped — per-tenant billing is instance-based, not database-based. 50 databases on one db-g1-small: ~$25/month. Scale requires instance upgrades. | ~$50–200/month depending on instance tier |
| **Azure Flexible Server** | Shared instance per region | Same pattern as GCP — Flexible Server is instance-scoped. 50 databases on one B2s (2 vCPU, 4GB RAM): ~$55/month. | ~$55–150/month |

**Recommended.** For GrowDirect-managed deployments at 10–50 tenants: shared PostgreSQL host (RDS db.t3.small or equivalent), per-tenant databases. Aurora Serverless v2 is the upgrade path when workload patterns are spiky — the ACU auto-scaling eliminates over-provisioning. Isolated RDS instances per tenant are only warranted when a specific tenant's compliance or SLA requirement demands it.

---

## Decision Summary

| Decision | Recommendation | When to Revisit |
|---|---|---|
| Cloud platform | AWS (default for GrowDirect-managed; follow client requirements for self-hosted) | Client mandate or regulatory constraint forces another platform |
| PostgreSQL | RDS PostgreSQL 17 or shared EC2 Docker for ≤10 tenants | Aurora Serverless v2 when tenant count exceeds 10 |
| Valkey | In-container Valkey for ≤5 tenants; ElastiCache for higher scale | ElastiCache when stream consumer lag becomes observable |
| Ollama/inference | In-container CPU for ≤31 stores; EC2 g4dn Spot for batch embedding at scale | When embedding queue lags consistently or vault growth exceeds 10K chunks/month |
| Object storage | S3 Standard | No change unless multi-cloud mandate |
| Container runtime | Docker Compose on EC2 for ≤10 tenants; ECS on EC2 for ≥10 tenants | When operational overhead of Docker Compose exceeds ECS management cost |
| Tenant isolation | Per-database shared host | Per-instance isolation when compliance or SLA demands it |

---

## Related

- [[method/catz-method-detail]] — CDF phases and workstreams (WS1 — Architecture & Infra)
- [[method/data-economics]] — data egress economics, storage costs, own-your-data argument
- [[method/it-architecture-options]] — Phase II architecture evaluation framework

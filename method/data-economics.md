---
classification: confidential
owner: GrowDirect LLC
type: method-reference
---

# Data Ingress/Egress Economics and the Own-Your-Data Argument

The retailers most vulnerable to vendor lock-in are the ones who never thought about their data as an asset until they tried to move it.

This article makes three arguments in sequence: what retail data actually costs to store and process (the baseline that most retailers never see); how traditional LP and analytics vendors monetize custody of that data (the hostage dynamic); and why CATz and Canary represent a structurally different model. The crossover math is included. The numbers are estimates based on AWS us-east-1 pricing and typical SMB specialty retail transaction patterns — flag them as estimates when using them in client conversations, but don't soften the conclusion.

---

## Section 1: Cost Model Baseline

### Transaction Volume Assumptions

A typical SMB specialty retailer on NCR Counterpoint or a comparable POS system processes:

| Store Profile | Transactions/Day | Annual Volume |
|---|---|---|
| Low-volume (boutique, gallery, specialty wine) | 50–200 | 18,000–73,000 |
| Mid-volume (sporting goods, garden center, hardware) | 200–800 | 73,000–292,000 |
| High-volume (pet supply, pharmacy, specialty food) | 800–2,000 | 292,000–730,000 |

A representative working assumption for a mid-volume specialty retailer: **500 transactions/day/store**. Used below for the cost model. Adjust by multiplying or dividing by the actual volume tier.

### Data Types and Daily Ingest Volume

Each transaction in Counterpoint generates records across five data types:

| Data Type | Source | Typical Payload Size | Daily Ingest per Store (500 tx) |
|---|---|---|---|
| Transaction records (PS_DOC) | POS | 2–8 KB per transaction (line items, tenders, discounts, header) | ~2.5 MB/day |
| Item master updates (IM_ITEM) | Back-office | ~50–200 bytes per item updated; 0.1–1% of catalog per day | ~0.5 MB/day |
| Inventory snapshots | Back-office | ~200 bytes/SKU/store for full snapshot; typically daily | ~1.0 MB/day (5,000 SKUs) |
| Customer records (AR_CUST) | POS + CRM | ~500 bytes per customer update; 1–5% of active customers per day | ~0.25 MB/day |
| Price/promo updates | Back-office | ~100 bytes per item affected; intermittent | ~0.1 MB/day (average) |

**Total daily ingest per store (estimate):** ~4.35 MB uncompressed. PostgreSQL with standard compression achieves 60–70% compression on this data type — actual on-disk footprint: ~1.5–1.75 MB/day/store.

### Monthly Retention Footprint

| Store Count | Daily Ingest (compressed) | Monthly Footprint | Annual Footprint | 3-Year Footprint |
|---|---|---|---|---|
| 5 stores | ~8.75 MB/day | ~262 MB | ~3.2 GB | ~9.6 GB |
| 15 stores | ~26.25 MB/day | ~787 MB | ~9.6 GB | ~28.7 GB |
| 31 stores | ~54.25 MB/day | ~1.6 GB | ~19.8 GB | ~59.4 GB |

These are database-resident estimates. Object storage (vault snapshots, transaction exports) adds ~20–30% on top of the database footprint.

### Cost to Store This Data (AWS us-east-1, estimates)

**RDS PostgreSQL gp3 storage:** $0.115/GB-month.
**S3 Standard (object storage, backups):** $0.023/GB-month.

| Store Count | 3-Year DB Storage | Monthly DB Storage Cost | 3-Year Object Storage | Monthly Object Storage Cost | Total Monthly (steady-state) |
|---|---|---|---|---|---|
| 5 stores | 9.6 GB | ~$1.10/month | ~3 GB | ~$0.07/month | ~$1.17/month |
| 15 stores | 28.7 GB | ~$3.30/month | ~9 GB | ~$0.21/month | ~$3.51/month |
| 31 stores | 59.4 GB | ~$6.83/month | ~18 GB | ~$0.41/month | ~$7.24/month |

This is the storage cost for three years of retail transaction data at mid-volume specialty retail. At 31 stores: **~$7/month.** Not $7/store. $7 total.

### Egress Cost: Sending Data to a SaaS LP Vendor

If a retailer sends their transaction data from their cloud environment to a third-party SaaS LP platform, that outbound transfer is billed by the cloud provider.

AWS us-east-1 egress to internet: **$0.09/GB** (first 10TB/month).

| Store Count | Monthly Data Transfer to Vendor | Monthly Egress Cost (AWS) |
|---|---|---|
| 5 stores | ~262 MB/month | ~$0.02/month |
| 15 stores | ~787 MB/month | ~$0.07/month |
| 31 stores | ~1.6 GB/month | ~$0.14/month |

Cloud egress for sending this data *out* is trivial. The story reverses when you want the data *back*.

### Compute Cost for Detection Rule Evaluation (Module Q Workload)

The Chirp detection engine (Module Q) evaluates every transaction against the active rule catalog. At 500 transactions/day/store, this is a lightweight continuous workload — not a batch job, not a reporting ETL.

Rule evaluation per transaction: ~1–5ms CPU time (single rule evaluation; 37 rules in the standard catalog = ~40–185ms per transaction). At 500 transactions/day: ~22–92 CPU-seconds/day/store.

On an EC2 t3.micro (2 vCPU, 1GB RAM, ~$7.50/month), this workload uses <1% of available compute at 31 stores. Detection rule evaluation is not the cost driver in this architecture. Data persistence is not the cost driver either. The compute and storage costs at SMB scale are genuinely small.

The cost driver, for retailers paying SaaS LP vendors, is the subscription fee — not the infrastructure.

---

## Section 2: The Data Hostage Dynamic

Traditional LP and analytics vendors operate a specific business model. Understanding it is not optional for a retailer evaluating platforms.

### How the Model Works

**Ingestion is free or cheap.** The vendor integrates with your POS, pulls the data, and charges a modest "setup fee" or nothing at all. This is the hook. Getting your data into their system has been made as frictionless as possible.

**The subscription is the rent.** Typical SaaS LP platform pricing for a 15–30 store specialty retailer runs $200–600/store/month for an LP analytics and case management platform. At 31 stores: $6,200–$18,600/month. The retailer pays this every month, indefinitely. The data lives on the vendor's servers.

**Extraction is where the billing clock runs.** Want a bulk export of your 3-year transaction history? That's a professional services engagement, billed at $150–250/hour. Want to pull your case management data to a new platform? That may not be possible — the case records are in a proprietary schema that doesn't export cleanly. Want your detection rule library back? Rules are typically vendor-proprietary and not transferable. Want your audit trail for a litigation matter? Prepare to negotiate.

**The migration cost is priced to discourage leaving.** A retailer who has been on a SaaS LP platform for 3 years and decides to switch faces:

1. **Egress fees on historical data** — if the vendor charges for bulk data export (many do), the cost scales with how long the retailer has been on the platform. The longer you stay, the more expensive it becomes to leave.
2. **Proprietary rule formats** — detection rules written in the vendor's rule language don't port to another platform. Three years of LP team refinement walks out the door.
3. **Case management history locked in** — without case history, the new platform starts blind. No historical patterns, no baseline for what "normal" looks like for this retailer.
4. **Audit trail in vendor custody** — a forensic audit trail that lives on a vendor's servers, in a format only they can read, is not a forensic audit trail that will satisfy a serious compliance or legal inquiry. It's a vendor-controlled document.
5. **Re-integration cost** — the new platform has to re-ingest 3 years of transaction data from scratch, if the retailer can even get it in a usable format.

The result: **the retailer has paid 3 years of subscription fees and is now more locked in than when they started.** The vendor's pricing structure is a compounding switching cost. This is not an accident. It is the business model.

### At What Store Count Does "Run It Yourself" Beat "Pay the SaaS Vendor"?

This is the crossover calculation. The comparison is:

- **SaaS LP platform cost:** $200–600/store/month (estimate; varies by vendor, contract, and negotiation)
- **CATz/Canary cost:** GrowDirect delivery engagement (one-time, CDF engagement) + monthly infrastructure + GrowDirect support

The infrastructure costs from Section 1 are a floor. The relevant comparison is the ongoing monthly cost differential.

| Store Count | SaaS LP Cost (low-end, $200/store) | SaaS LP Cost (high-end, $600/store) | Canary Infrastructure + Support (estimate) | Monthly Savings (mid-case) |
|---|---|---|---|---|
| 5 stores | $1,000/month | $3,000/month | ~$75–200/month | ~$1,500/month |
| 15 stores | $3,000/month | $9,000/month | ~$150–400/month | ~$5,600/month |
| 31 stores | $6,200/month | $18,600/month | ~$250–800/month | ~$11,900/month |

These are estimates. The Canary infrastructure + support number includes: managed cloud infrastructure (shared or isolated per tenant), GrowDirect ongoing support engagement, and software maintenance. It does not include the one-time CDF engagement cost, which is amortized over the subscription savings.

**The crossover is not at 31 stores. The crossover is at the first store.** The economics favor owning your infrastructure at any meaningful scale. The reason most retailers don't make this choice is not cost — it's complexity. CATz is the method that removes the complexity barrier.

### The Data Custody Distinction

There is a structural difference between data that lives on your infrastructure and data that lives on a vendor's infrastructure. For most software categories, this distinction doesn't matter much. For LP and compliance data, it matters considerably.

**Forensic audit trail.** The RaaS module in Canary produces Bitcoin ordinals inscriptions of Merkle-batched event hashes. This is a public, tamper-evident audit trail. A vendor-hosted audit trail is only as trustworthy as the vendor — and the vendor has an interest in how that audit trail reads in a dispute with you.

**Compliance posture.** PCI DSS Requirement 9.4 requires that transaction records be retained for 12 months with the last three months immediately available. A retailer who relies on a SaaS LP vendor to satisfy this requirement is delegating a compliance obligation to a third party — and accepting that third party's data residency, encryption, and access control choices. That delegation has to be documented and audited.

**Right-to-delete (GDPR/CCPA).** When a customer exercises their right to erasure, the retailer must demonstrate that all personal data has been deleted. If customer data is in a vendor's system, the retailer cannot independently verify deletion — they have to trust the vendor's attestation. This is a compliance exposure that gets larger as privacy regulations tighten.

---

## Section 3: GrowDirect's Positioning

CATz is the delivery method. Canary is the platform the retailer operates. GrowDirect earns on delivery (the CDF engagement) and ongoing support — not on data custody or extraction friction.

### What This Means in Practice

**The retailer's data is in their infrastructure from day one.** Every transaction record, every detection rule, every case file lands in a database that belongs to the retailer — either in their own cloud account or in GrowDirect-managed infrastructure under terms that give them full extraction rights. The data is theirs. The audit trail is theirs. The detection rule library is theirs.

**GrowDirect's business model is not hostage-dependent.** The SaaS LP vendor's business model requires that data extraction be expensive — otherwise the switching cost disappears and churn increases. GrowDirect's model is the opposite: make it easy to audit, export, and migrate. Retailer confidence in data ownership is a selling point, not a risk.

**The detection rule catalog is a portable asset.** Module Q rules are written against the canonical retail data model and documented in the retailer's vault. They are not locked in a proprietary rule format. An LP team that has been tuning their Chirp rules for 18 months has an asset — an articulated, documented set of detection logic that reflects their specific operating environment. They own it.

**The audit trail is public-verifiable.** Bitcoin ordinals inscriptions are externally verifiable without GrowDirect's involvement. The retailer can verify the integrity of their transaction record without asking GrowDirect's permission or trusting GrowDirect's attestation. This is structurally different from a vendor-controlled audit log.

### Why This Matters to a Skeptical CIO

A CIO evaluating LP platforms has been burned before. The patterns they watch for:

1. **Lock-in through data gravity** — the more data in the vendor's system, the harder it is to leave. CATz inverts this: the data stays on the retailer's side of the boundary. There is no accumulating data gravity pulling toward GrowDirect.

2. **Opaque rule logic** — vendors who say "we use proprietary algorithms" mean "you cannot audit what we're doing with your data." Canary's rule catalog is documented, version-controlled, and readable. The LP team can inspect every rule.

3. **Vendor dependency for compliance evidence** — any audit trail that requires a vendor to produce it is an audit trail the vendor controls. Bitcoin ordinals inscription means the integrity evidence is in a public ledger, not in GrowDirect's database.

4. **Platform pricing tied to store count** — per-store pricing at SaaS vendors means the cost scales linearly with the retailer's success. Canary's infrastructure cost scales sub-linearly: the marginal cost of store 16 is meaningfully less than the marginal cost of store 1.

### Why This Matters to a VAR (Rapid POS, MSP Model)

A VAR considering reselling Canary through a white-label or referral model faces a version of the same question: what does the business model look like for the merchants they serve?

If the VAR places merchants on a SaaS LP vendor, the VAR has introduced a dependency the merchant will eventually resent — and potentially blame the VAR for. The VAR's long-term margin is also limited: the SaaS vendor takes the subscription revenue, the VAR takes a referral fee, and the economic leverage is with the vendor.

If the VAR deploys Canary under a GrowDirect managed-infrastructure model, the merchant's data stays within a controlled environment, the VAR controls the relationship, and the economics of the engagement — delivery, support, expansion — accrue to the VAR and GrowDirect, not to a SaaS platform the VAR doesn't control.

The own-your-data argument is also a sales argument: a VAR pitching Canary to a merchant who has been burned by a previous platform can lead with "your data stays with you" as a differentiator. This is not a defensive claim. It is the reason a skeptical merchant says yes.

### The Honest Caveat

The own-your-data model transfers operational responsibility to the retailer or their managed service provider. A retailer who relies on a SaaS vendor has outsourced backup, uptime, patching, and security to that vendor. With Canary on managed infrastructure, GrowDirect carries some of that responsibility — and the retailer's team carries more than with a pure SaaS model.

This is the correct tradeoff for a retailer who values control, auditability, and cost efficiency over zero operational involvement. It is not the correct tradeoff for a retailer who genuinely wants someone else to own every operational detail. That segment exists. It is not CATz's primary market.

---

## Summary

| Factor | SaaS LP Vendor | CATz / Canary |
|---|---|---|
| Data location | Vendor infrastructure | Retailer-controlled or GrowDirect-managed with full extraction rights |
| Monthly cost at 31 stores | $6,200–$18,600 | ~$250–800 (infrastructure + support) |
| Detection rule portability | Proprietary, non-transferable | Documented in vault, portable |
| Audit trail | Vendor-controlled log | Bitcoin ordinals-inscribed, publicly verifiable |
| Switching cost | High and compounding | Low — data and rules are owned by the retailer |
| Compliance posture | Vendor attests to compliance | Retailer controls their own evidence |
| Operational responsibility | Fully outsourced | Shared (GrowDirect manages infrastructure; LP team owns rule tuning) |

The economics favor ownership at any meaningful scale. The method removes the complexity barrier. The data-hostage dynamic is the clearest argument for why a retailer who can run their own platform should.

---

## Related

- [[method/catz-method-detail]] — CDF phases and workstreams
- [[method/cloud-architecture-options]] — infrastructure cost reference, tenant isolation model
- [[cbm-v2/data-protection-and-governance]] — PII, hash-chain evidence, compliance posture
- [[about/growdirect-llc]] — GrowDirect's business model and positioning

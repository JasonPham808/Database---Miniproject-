<img width="1200" height="419" alt="image" src="https://github.com/user-attachments/assets/78ba1248-ee81-4fec-9415-32a259ecf80f" />

# Mini Project – AAMI Insurance Operations (Policy & Claims Lifecycle)
## What have I done?
- Analysed end‑to‑end insurance operations for AAMI, covering policy management, customer management, claims processing, payments/billing, discounts, and SME business insurance.
- Mapped key processes such as new policy application, endorsements, renewals/cancellations, claim lodgement and assessment, express settlements, and premium payment workflows.
- Identified data entities and business rules for premium calculation, discount eligibility, risk profiling, and policy–customer–claim relationships to support AI/automation opportunities.
- Highlighted automation use cases (e.g., express claims, reminders, discount assignment) to inform potential AI solutions for operational efficiency and improved customer experience.
## Overview of the company AAMI (Australian Associated Motor Insurers Limited)
**Company Overview**  
- Leading Australian insurer for individuals/SMEs; motor, home/contents, landlord, travel, business, life/income protection, pet, CTP products.  
- Multi-channel: online portals, phone support.

**Key Data Entities**
- **Customer**: Profiles (personal/business details, contacts, preferences), multi-policy links, account status.  
- **Policy**: Type (car/home/business), coverage details, premiums (risk-based calc: assets/drivers/location/claims), excess, payment plans, dates (effective/expiry). 
- **Claims**: Lodgement (incidents/evidence), assessment (damage/validity/quotations), settlement (approval/payment/repairs), express claims, tracking.  
- **Payments/Billing**: Premiums (full/installments), excess, refunds/adjustments, due dates, automated reminders/overdues.  
- **Discounts**: Types (loyalty/multi-policy/online), eligibility rules, validity periods, auto-calc at issuance/renewal.  
- **Business Insurance**: Liability, interruption, property/tools coverage; combinable with home packages.  
**Core Processes/Use Cases**  
- **Policy Lifecycle**: Application/issuance, endorsements (add/remove items/drivers), renewals/cancellations, premium recalc.  
- **Claims Workflow**: Report/submit → assess → authorize/settle → track docs.  
- **Customer Interactions**: Support inquiries, complaints, and policy advice via integrated data views.  
- **Automation Opportunities**: Express settlements, discount assignment, payment reminders, risk profiling.

## AAMI Insurance Business Rules (Database Modeling)
**Unique Identifiers & Entities**  
- Customers: Unique **CustomerID** (personal/contact info).  
- Policies: Unique **PolicyID** → 1 Customer.  
- CoveredItems: Unique **CoveredItemID** → 1 Policy (cars/homes/assets).  
- Claims: Unique **ClaimID** → 1 Policy.  
- Discounts: Unique **DiscountID** → Many Policies.  
- ClaimHandlers: Unique **StaffID** → Many Claims.  
**Relationships & Cardinalities**  
- 1:N: Customer→Policies, Policy→CoveredItems, Policy→Claims.  
- 1:N: Discount→Policies (or M:N via junction).  
- N:1: Claims→Staff (one handler per claim).  
**Atomicity & Dependencies**  
- Atomic fields only (split names, single contacts).  
- No repeating groups; no partial/transitive deps.  
- Independent data → separate entities (discounts, handlers).  
**Policy Rules**  
- PolicyStatus: active/expired/cancelled.  
- CoveredItems: rego/address/make/model/year (risk/premium calc).  
- Claims: status/outcomes/timestamps (incident/lodgement).  
- Discounts: eligibility rules/duration.  
**Integrity Constraints**  
- FK referential integrity (Claims→valid Policies).  
- Date logic: renewal/expiry consistency; claims→active policies.  
**Privacy**: Encrypt PII (contacts/IDs); access controls.

## Dependency Diagram & Normalization: 1NF → 3NF
<img width="963" height="315" alt="image" src="https://github.com/user-attachments/assets/982c6657-6341-4dcb-9aa3-60f38b4e66b0" />

### 1NF Status
- **Atomic attributes**: Customer_Name, Amount (no multi-valued fields)
- **Single-column PKs**: Customer_ID, Claim_ID, Covered_Item_ID
### Anomalies Identified
- **Insertion**: Discounts require policy existence
- **Update**: Multi-row discount propagation → inconsistency risk
- **Deletion**: Policy deletes orphans' discount data
### Root Causes
- **Redundancy**: Repeated discount details across records
- **Transitive Dependencies**: 
  - DiscountDescription → DiscountID
  - ClaimHandlerName → Staff entity (3NF violation)

### Normalization Path
- **2NF**: Achieved (no partial dependencies, single PKs)
- **3NF**: Extract Discount/ClaimHandler entities

## 2NF Status
<img width="1156" height="454" alt="image" src="https://github.com/user-attachments/assets/4b5f2714-2f2c-4ee1-8060-8f567fb14801" />

### Partial Dependency Anomalies (Avoided)
- **Insertion**: No dummy/nulls for partial-key attrs  
- **Update**: No multi-tuple propagation risks  
- **Deletion**: No orphaned partial-key data  

## 3NF Status
### Transitive Dependency Anomalies (RESOLVED)
- **Insertion**: Discounts now independent of policies ✓
- **Update**: Single discount update propagates via FK ✓  
- **Deletion**: Policy delete preserves discount data ✓

## Entity Relationship Diagram for the company AAIM
<img width="871" height="405" alt="image" src="https://github.com/user-attachments/assets/9c42f573-b471-4eff-8f07-8634072dd955" />

**The Entity-Relationship Diagram (ERD)** for AAMI incorporates a CUSTOMER_CLAIM associative entity to resolve the many-to-many relationship between Customer and Claim, converting it into two one-to-many relationships. This supports realistic insurance scenarios, such as joint claims and multiple insured parties, where each claim involves one or more customers, and each customer may have multiple claims.
**Key relationships include**:
- Customer → CoveredItem (1:N): One customer insures multiple assets; each item has single ownership
- CoveredItem → Claim (1:N): Multiple claims possible per asset over time
- Claim → Discount (N:1, optional): Efficient discount sharing reduces redundancy
- Claim → ClaimHandler (N:1): Single handler accountability
- Participation constraints: Mandatory (CoveredItem→Customer, Claim→≥1 Customer via assoc entity); optional (Claim→Discount). This normalized, scalable ERD enables effective policy management and claims administration for AAMI's operations




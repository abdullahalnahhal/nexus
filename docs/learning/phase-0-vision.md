# NEXUS — Learning Notes

# Phase 0 — Vision & Business Discovery

## 1. What This Phase Was Really About

The purpose of Phase 0 was not to design the database or start coding.

The purpose was to learn how to understand a business system before designing its technical solution.

The working sequence became:

```text
Business Understanding
        ↓
Business Concepts
        ↓
Business Rules
        ↓
Domain Model
        ↓
Architecture
        ↓
Implementation
```

---

## 2. Business First

A major lesson was the difference between:

> "What tables do we need?"

and:

> "What business concepts actually exist?"

For example, POS is not merely a database table.

It represents an operational business point with:

* Wallet
* Shifts
* Sales
* Returns
* User assignments
* Business restrictions

---

## 3. Ownership vs Association

A major discovery was that not every relationship means ownership.

Examples:

```text
Branch → POS
Branch → Warehouse
```

represent strong structural relationships.

But:

```text
User ↔ Branch
User ↔ POS
```

represent operational access/assignment relationships.

A User can work across multiple Branches and POSes without belonging exclusively to one.

---

## 4. Role vs Permission vs Assignment

Another important lesson:

These are different concepts.

### Role

Describes the user's business responsibility.

### Permission

Describes what actions the user is allowed to perform.

### POS Assignment

Describes which POSes the user may operate and potentially whether the user can sell on them.

Therefore:

```text
User
 ├── Role
 ├── Permissions
 └── POS Assignments
```

should not automatically be collapsed into one concept.

---

## 5. Shift as a Business Concept

The Shift initially looked like a time period.

Domain discovery showed that it is much more important.

A Shift represents an operational and financial accountability period for a POS.

It controls:

* Assigned personnel
* POS operation
* Financial closing
* Settlement
* REMAIN
* Confirmation before the next Shift

This is an example of discovering a domain concept through business behavior rather than through data fields.

---

## 6. Financial Effects Are Not Just Balances

A key lesson from the Sale flow:

A Sale may produce different financial effects.

Example:

```text
Sale Total = 1,000
Paid = 700
Remaining = 300
```

The system should conceptually represent:

```text
POS receives 700
Customer owes 300
Branch has a receivable of 300
```

The 300 is not physical cash.

Therefore:

> A financial balance and a financial claim are not necessarily the same thing.

---

## 7. Business Rules Should Be Explicit

Rules discovered during conversation should not disappear inside implementation details.

They are documented separately and receive stable IDs.

Example:

```text
BR-024 — Blocked Customer

A Blocked customer cannot make a Sale
until the block is removed.
```

Later, these rules can be traced to:

```text
Business Rule
    ↓
Domain/Application Logic
    ↓
Automated Test
```

---

## 8. Domain Map vs Business Rules vs Glossary

Three documentation artifacts have different responsibilities.

### Domain Map

Answers:

> What concepts exist and how are they related?

### Business Rules

Answers:

> What must or must not happen?

### Glossary

Answers:

> What does each business term mean specifically in NEXUS?

This separation keeps the documentation focused.

---

## 9. Important Discovery Method

A useful technique discovered during Phase 0 is to ask:

* What is this concept?
* Why does it exist?
* What can it do?
* What can it not do?
* What does it interact with?
* What happens before it?
* What happens after it?
* What rules constrain it?
* Who is responsible for it?

The answers gradually reveal the Domain Model.

---

## 10. Current Staff-Level Learning Goal

The purpose of NEXUS is not only to build a working application.

It is also a practical exercise in Staff-level engineering thinking:

* Understanding business domains
* Identifying boundaries
* Modeling business behavior
* Making rules explicit
* Separating ownership from association
* Identifying invariants
* Designing around business capabilities
* Connecting business rules to implementation and tests

The target is to move from:

> "I know how to implement the feature."

toward:

> "I understand the business problem, can model it, identify its constraints, and design a sustainable solution."

---

## 11. Current Discovery State

Phase 0 Vision is considered complete.

Phase 0.2 Domain Discovery is in progress.

Current discovered concepts include:

* Branch
* Warehouse
* POS
* User
* Role
* Permission
* POS Assignment
* Shift
* Manager
* Salesman
* Sale
* Return
* Customer
* Customer Grade
* POS Wallet
* Branch Wallet
* Customer Receivable

Online Customer and Online Warehouse are intentionally deferred.

---

## Phase 0.2 — Inventory Discovery

### 1. Domain Discovery Before Implementation

Business Understanding
→ Business Concepts
→ Business Rules
→ Domain Model
→ Implementation

We do not start with database tables or classes.

### 2. Product Taxonomy

Inventory can be organized through:

Category
→ Subcategory
→ Product

### 3. Attribute Inheritance

Category can define Attribute Definitions.

Subcategory inherits and may add.

Product inherits and may add Product-specific Attributes.

### 4. Product vs Variant

A Variant is a concrete configuration of a Product.

Every Product has one automatically-created Primary Variant.

The Primary Variant is a real stock-bearing Variant.

Additional Variants are created only when needed.

### 5. Dynamic Attributes

Current types:

- TEXT
- NUMBER
- DATE
- SELECT
- MULTI_SELECT
- BOOLEAN

Any supported type may be Variant-Defining.

### 6. Variant Identity

Variant identity is determined by Variant-Defining Attribute values.

The same complete combination cannot occur twice within one Product.

### 7. Actual Variants Only

NEXUS does not generate all possible combinations.

The User creates only the actual Variants required.

### 8. Stock as Current State

Stock is:

> The current physical quantity of a Product Variant in a Warehouse.

Reserved/Damaged/Expired are not modeled as Stock Details.

### 9. Wastage/Loss

Wastage/Loss is separate from current Stock.

When goods are written off:

- Stock decreases.
- The reason is recorded separately.
- The historical event belongs to future Wastage/Loss / Stock Movement modeling.

---

# References — What We Learned From Each

## REF-IND-001 — GS1 Global Data Model

**Source:** GS1 Global Data Model

**What we learned:**
- Product master data naturally uses Attributes.
- Product data can contain common/foundational attributes.
- Attribute modeling is an established product-data concern.

**What we used:**
- Product Attributes.
- Attribute Definitions.
- Category-aware product data.

**What we did NOT take:**
- GS1's exact hierarchy.
- GS1's exact attribute catalog.
- GS1's exact implementation.

---

## REF-IND-002 — GS1 Global Product Classification

**What we learned:**
- Product classification can be hierarchical.
- Different categories can have different characteristics.

**What we used:**
- Category.
- Subcategory.
- Category-specific Attribute thinking.

**What remains NEXUS-specific:**
- Our exact Category/Subcategory structure.
- Our inheritance behavior.

---

## REF-IND-003 — GS1 Attributes vs Trade Item Attributes

**What we learned:**
- Classification attributes and actual product attributes are conceptually different.

**What we used:**
- Separation of Category-level and Product-level Attributes.
- Attribute inheritance concept.

**NEXUS-specific:**
- Category → Subcategory → Product additive inheritance.

---

## REF-IND-004 — Google Product Variant Structured Data

**What we learned:**
- Product Groups can contain Variants.
- Some properties are common.
- Some properties determine variation.

**What we used:**
- Product / Variant distinction.
- Variant-defining Attributes.

**NEXUS-specific:**
- Primary Variant.
- Automatic Primary Variant creation.
- User-created actual Variants.
- Variant Stock ownership.

---

## REF-ACAD-001 — Schrady (1970)

**What we learned:**
- Inventory records should correspond meaningfully to physical inventory.
- Inventory record accuracy is an operational concern.

**What we used:**
- Grounding the concept:

`Stock = Current Physical Quantity`

**Not derived from it:**
- Our exact Stock entity.
- Our future Stock Movement model.

---

## REF-ACAD-002 — Herrero-Vidal et al. (2024)

**What we learned:**
- Product variants can be represented through variation attributes.

**What we used:**
- Product / Variant relationship.
- Variant-defining characteristics.

**Not derived from it:**
- Primary Variant.
- Attribute inheritance.
- Stock model.

---

## REF-ACAD-003 — Rekik et al. (2025)

**What we learned:**
- Recorded and physical inventory can diverge.
- Perishability and stock counting affect inventory accuracy.

**What we used:**
- Future investigation of Stock Counts.
- Future investigation of perishability.

**Still Open:**
- Stock Count.
- Expiry tracking.

---

## REF-ACAD-004 — Sasanuma et al. (2021)

**What we learned:**
- Wastage is a meaningful concept distinct from ordinary inventory.

**What we used:**
- Separation:

Current Stock ≠ Wastage/Loss

**Not derived from it:**
- Our Wastage workflow.
- Our Stock Movement taxonomy.

---

# Reference Discipline

For every major future decision:

Reference
↓
What we learned
↓
What we used
↓
What remains NEXUS-specific

---

## Phase 0.2 — New Learning: Supply Chain & Inventory Discovery

### 10. Inventory Is Not an Isolated Domain

A major discovery was that Inventory cannot be modeled independently from the business processes that cause Stock to change.

The discovery path became:

Supply Chain
      ↓
Supplier
      ↓
Purchase
      ↓
Warehouse
      ↓
Stock
      ↓
Stock Movement

This showed that Stock is a **current state**, while the business processes explain how that state changes.

---

## 11. Financial Effect ≠ Inventory Effect

A major discovery from Supplier Returns:

A Stock movement and its financial consequence do not necessarily have the same value.

Example:

Original Purchase Value = 2,000
Supplier Return Value   = 1,200

The Stock movement is based on the returned quantity.

The financial settlement is determined separately by the Supplier Return Invoice.

Therefore:

> **Do not automatically derive financial consequences from inventory quantity movements.**

---

## 12. Document vs Transaction

NEXUS exposed an important distinction:

Business Document
        ↓
defines what happened

versus:

Financial Transaction
        ↓
records movement of money

For example:

Purchase Invoice
Supplier Return Invoice
        │
        ▼
Financial consequences

while:

Supplier Payment
        │
        ▼
Actual financial transaction

A Payment can then be allocated to multiple documents.

---

## 13. Attribution Is Not Ownership

Supplier Representative balances revealed another important domain-modeling lesson.

A Representative can have an attributed amount without actually owning an independent financial balance.

Supplier Company
      │
      └── Actual Debt
             │
             ├── Branch Attribution
             └── Representative Attribution

This prevents accidentally modeling every visible balance as a separate financial liability.

---

## 14. Stock Movement as a Historical Explanation

Current Stock:

Stock = Current Physical Quantity

Historical movements:

Purchase
Sale
Transfer
Damage
Missing
Return
Manual Edit

Therefore:

Current State
     +
Historical Business Events

are separate concepts.

---

## 15. Transfer Is a Workflow, Not Just a Quantity Change

A Transfer initially looks like:

Warehouse A → Warehouse B

Domain discovery showed that there are actually two possible initiation workflows:

Destination Request
       ↓
Source Approval

or:

Source Order
       ↓
Destination Approval

Only after the appropriate approval does the inventory movement execute.

This is an example of discovering **business workflow before modeling persistence**.

---

## 16. Return Is Not Always Reversal

A Supplier Return cannot simply be modeled as:

Purchase
   ↓
Reverse Purchase

because:

- Return value may differ from purchase value.
- The financial settlement may be cash.
- The financial settlement may be an offset.
- Replacement is a separate business document.

Therefore:

> **Return is its own business document and process.**

---

## 17. Replacement Is a Separate Concept

Replacement was identified but intentionally deferred.

Current decision:

Supplier Return
        ≠
Replacement

Supplier Return uses:

Supplier Return Invoice

Replacement will later use:

Replacement Document

This prevents prematurely coupling two different business processes.

---

## 18. Current Phase 0.2 Discovery State

### Confirmed

- Product → Variant → Stock
- Stock is Variant-based.
- Stock is Warehouse-specific.
- No Stock Details concept.
- No Reserved Quantity.
- Supplier Company.
- Supplier Branch.
- Branch Reference Person.
- Branch Manager.
- Branch Representative.
- Supplier Opening Balance.
- Purchase Invoice = Goods Receipt.
- Mandatory original Purchase Invoice attachment.
- Supplier Return Invoice.
- Supplier Return can have a value different from original purchase value.
- Supplier Return affects Stock through `Upload - Supplier Returns`.
- Return financial treatment is determined by the Return Invoice.
- Replacement is deferred.
- Supplier Payments support Cash, Visa, Bank Transfer, Electronic Wallet.
- Non-cash payment requires evidence.
- Payment can be allocated across multiple Purchase Invoices / Supplier Receipts.
- Payment cannot exceed amount due.
- Transfer has two approval directions.
- Destination Warehouse does not need Branch ownership.
- Sales use the Branch Main Warehouse.
- Damage / Miss / Manual Edit movements exist.
- Manual Edit requires Warehouse Manager approval.

# Phase 0.2 — Inventory Discovery Learning
## Checkpoint 0.2-A

### 19. Business Documents vs Inventory Movements

A major discovery was that a Business Operation and its Inventory Effect are not the same concept.

The business operation is represented by a Business Document.

The resulting quantity change is represented by an Inventory Movement.

Therefore:

```text
Business Operation
        ↓
Business Document
        ↓
Inventory Movement
        ↓
Current Stock
```
This prevents the Inventory domain from becoming responsible for every business process that happens to change Stock.

---
### 20. Current State vs Historical State

NEXUS requires both:

```text
Current Stock
```
and:
```text
Inventory Movement History
```
Current Stock provides the operational state.

Inventory Movements explain how that state was produced.

Therefore:

> Current State and Historical Record have different responsibilities.

---

### 21. Quantity vs Cost

Another important discovery was the separation between Inventory and Commercial information.

Inventory Movement:

```text
Quantity
```
Business Document / Invoice:
```text
Quantity + Cost Information
```
This prevents Inventory from becoming implicitly coupled to costing and financial valuation.

---

### 22. No Reservation Means Simpler Availability

NEXUS currently has no Reserved Stock.

Therefore:
```text
Available Stock = Current Stock
```
This is an explicit scope decision.

It is not an assumption that reservation can never be introduced later.

---

### 23. Permission Is More Important Than Job Title

A major correction to the earlier domain language was:

"Manager can do X"

is not a sufficiently precise business rule.

The better model is:
```text
User
  ↓
Permissions
  ↓
Business Capabilities
```

A User may have a Manager role but not have a specific Permission.

Another User may have the Permission without having the Manager title.

Therefore:

> Authorization rules should be expressed in terms of Permissions.

---

### 24. Immutable History Through Corrective Movements

When a Final or Approved document is modified by an authorized User, the original Inventory Movement is not rewritten.

```text
Instead:

Original Movement
       +
Corrective Movement
       =
New Effective State
```

This preserves historical integrity and provides a traceable correction path.

---
### 25. Product–Warehouse Setup Is a Prerequisite

The existence of a Product does not automatically mean that the Product can move through every Warehouse.

The Product must first be added to the Warehouse.

That action automatically establishes:

```text
Product + Warehouse
        ↓
Product–Warehouse Setup
        ↓
Stock Context
```

This creates a clear boundary between:

* being a Product in the catalog
* being managed as Inventory in a specific Warehouse

---

### 26. Deactivation Does Not Mean Deletion

A Product–Warehouse Setup may become inactive.

However:
```text
Inactive
```
does not mean:
```text
Deleted
```
Historical documents and Inventory Movements remain.

The system records a change of state rather than destroying history.

---
## 27. Transfer Atomicity

A Transfer is not simply two independent stock updates.

It is one business operation producing two Inventory effects:
```text
Source Warehouse      -Q
Destination Warehouse +Q
```
Both must succeed together.

This introduced an important consistency invariant:

> A Transfer cannot be partially executed.

---

## 28. Reconciliation Is a Business Document

When Current Stock needs correction, NEXUS does not directly mutate Stock outside the normal Inventory mechanism.

Instead:
```text

Stock Reconciliation
        ↓
Corrective Movement
        ↓
Current Stock
```
This preserves the historical explanation of Stock changes.

---
## 29. Scope Is a Design Decision

The following are intentionally outside the current Inventory model:

* Reserved Stock
* Batch / Lot tracking
* Serial Number tracking
* Expiry tracking
* Multiple UOM
* UOM Conversion
* In-Transit Inventory
* Cost inside Inventory Movement

These may become future capabilities, but they are not current requirements.

---
## 30. Discovery Discipline

A new lesson from this checkpoint is the importance of distinguishing:
```text
Confirmed Rule
        vs
Historical Rule
        vs
Superseded Rule
        vs
Open Question
```
When a new discovery changes an earlier assumption, the old documentation should not be silently erased.

Instead:
```text
Previous Decision
       ↓
New Discovery
       ↓
Explicit Superseding Decision
```
This preserves the evolution of the Domain Discovery process.

---
## 31. Current Inventory Discovery State
### Confirmed
* Nine independent Inventory business documents.
* Permission-based authorization.
* Final documents for Sales/Purchase/Returns.
* Approval-controlled documents for Transfer/Adjustment/Loss/Write-off/Opening Balance.
* No Negative Stock.
* No Reserved Stock.
* Product + Warehouse Inventory identity.
* One Unit of Measure per Product.
* Quantity-only Inventory Movement.
* Cost remains in Business Documents / Invoices.
* Persisted Current Stock.
* Historical Inventory Movements.
* Product–Warehouse Setup prerequisite.
* Automatic Product–Warehouse Setup creation.
* Logical Deactivation.
* Zero Stock required before Product–Warehouse Deactivation.
* Warehouse-to-Warehouse Transfer only.
* Atomic Transfer.
* No In-Transit Inventory.
* Corrective Inventory Movements.
* Permission-controlled Reconciliation.

---
##Still Open
* Customer Return detailed rules.
* Supplier Return detailed rules.
* Return references.
* Partial Returns.
* Opening Balance recurrence.
* Quantity Adjustment semantics.
* Loss vs Write-off / Depreciation distinction.
* Reconciliation details.
* Approval Log structure.
* Exact multi-line validation timing.

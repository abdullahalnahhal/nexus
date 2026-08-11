# NEXUS — References

## Domain-Driven Design

Evans, E. (2003).
Domain-Driven Design: Tackling Complexity in the Heart of Software.
Addison-Wesley.

Primary concepts used:
- Domain Model
- Entity
- Value Object
- Aggregate
- Bounded Context
- Ubiquitous Language

---

## Domain Modeling

Fowler, M.
Domain Model.

Concept applied:
- Modeling business behavior and concepts before implementation.

---

## Event Storming

Brandolini, A.
Event Storming.

Concepts:
- Business Events
- Business Processes
- Domain Discovery

---

## Requirements Engineering

Sommerville, I.
Software Engineering.

Concepts:
- Requirements
- System Modeling
- Software Architecture

---

## Reference Classification

Industry / Standard
→ terminology, standards, established models

Academic / Research
→ research and theoretical grounding

NEXUS Decision
→ business decision discovered specifically for NEXUS

---

# Industry References

## REF-IND-001 — GS1 Global Data Model

Source:
GS1 Global Data Model

https://ref.gs1.org/standards/gdm/

### Provides

Standardized product master data and product attributes.

### We learned

- Product information can be modeled through Attributes.
- Product data has common/foundational attributes.
- Attribute modeling is a recognized master-data concern.

### Used for

- Product Attributes
- Attribute Definitions
- Category-aware product data

### Does NOT decide

- NEXUS hierarchy
- NEXUS inheritance
- Primary Variant
- NEXUS Stock model

---

## REF-IND-002 — GS1 Global Product Classification

https://www.gs1.org/standards/gpc/how-gpc-works

### We learned

- Classification hierarchy.
- Category-specific characteristics.

### Used for

- Category
- Subcategory
- Category-specific Attribute thinking

### Does NOT decide

NEXUS's exact classification tree.

---

## REF-IND-003 — GS1 GPC Attributes vs Trade Item Attributes

https://support.gs1.org/support/solutions/articles/43000734162-what-is-the-difference-between-gpc-brick-attributes-and-gds-trade-item-attributes-

### We learned

Classification-level Attributes and actual product/trade-item Attributes are conceptually different.

### Used for

- Category Attributes
- Product Attributes
- Attribute inheritance thinking

### NEXUS-specific

Category → Subcategory → Product additive inheritance.

---

## REF-IND-004 — Google Product Variant Structured Data

https://developers.google.com/search/docs/appearance/structured-data/product-variants

### We learned

- ProductGroup
- Variants
- Common properties
- Variation-determining properties
- Variant relationships

### Used for

- Product / Variant
- Variant-defining Attributes

### NEXUS-specific

- Primary Variant
- Automatic Primary Variant
- Actual Variants only
- Variant Stock

---

# Academic References

## REF-ACAD-001 — Schrady (1970)

Operational definitions of inventory record accuracy.

Naval Research Logistics Quarterly, 17(1), 133–142.

DOI:
10.1002/nav.3800170113

https://onlinelibrary.wiley.com/doi/10.1002/nav.3800170113

### Used for

Grounding:

Stock = Current Physical Quantity

---

## REF-ACAD-002 — Herrero-Vidal et al. (2024)

Learning variant product relationship and variation attributes from e-commerce website structures.

https://arxiv.org/abs/2410.02779

### Used for

- Variant relationships
- Variation Attributes
- Common vs varying information

---

## REF-ACAD-003 — Rekik et al. (2025)

Inventory record inaccuracy in grocery retailing.

https://arxiv.org/abs/2506.05357

### Used for

- Inventory accuracy
- Physical vs recorded stock
- Future Stock Count investigation
- Future perishability investigation

---

## REF-ACAD-004 — Sasanuma et al. (2021)

An opaque selling scheme to reduce shortage and wastage in perishable inventory systems.

https://arxiv.org/abs/2112.02660

### Used for

Understanding Wastage/Loss as a concept separate from ordinary inventory availability.

---

# Reference → NEXUS Decision Map

| NEXUS Concept | Reference | Support |
|---|---|---|
| Product Attributes | REF-IND-001 | Industry |
| Category-specific Attributes | REF-IND-001 / 002 | Industry |
| Classification | REF-IND-002 | Industry |
| Product Attributes vs Classification Attributes | REF-IND-003 | Industry |
| Product / Variant | REF-IND-004 / ACAD-002 | Industry + Academic |
| Variant-defining Attributes | REF-IND-004 / ACAD-002 | Industry + Academic |
| Primary Variant | NEXUS Decision | Business |
| Actual Variants Only | NEXUS Decision | Business |
| Variant owns Stock | NEXUS Decision | Business |
| Stock = Physical Quantity | ACAD-001 / ACAD-003 | Academic |
| No Stock Details | NEXUS Decision | Business |
| Wastage/Loss | ACAD-004 + NEXUS Decision | Background + Business |
| Stock Movement | Open Question | Not decided |

---

## Phase 0.2 Reference Update

In the current phase, NEXUS must distinguish between:

1. What was learned from external references.
2. What was decided as a NEXUS Business Rule.

The external references provide concepts, principles, and industry knowledge.

They do not dictate the exact business behavior of NEXUS.

---

## Reference → Learning → NEXUS Decision

| Reference / Concept | What We Learned | NEXUS Use |
|---|---|---|
| Domain-Driven Design — Eric Evans | Business concepts and behavior should drive the model | Supplier / Purchase / Return / Payment are modeled as business concepts |
| Event Storming — Alberto Brandolini | Business events and workflows help reveal domain behavior | Transfer approval flows and Stock Movements |
| Requirements Engineering — Sommerville | Requirements should be explicitly modeled and traced | Business Rules IDs and Open Rules |
| Inventory Record Accuracy research | Recorded inventory must be considered against physical inventory | Stock represents current physical quantity |
| Perishable Inventory research | Perishable goods create distinct inventory/wastage concerns | Supports future expiry/wastage discovery |
| GS1 Product Data references | Product data and attributes are structured business information | Existing Product / Attribute discovery |
| Product Variant research | Variants can be distinguished by variation attributes | Existing Variant model |

---

## Important Classification

Reference
    ↓
What we learned
    ↓
NEXUS interpretation
    ↓
NEXUS Business Decision

We must not write:

> "The reference says NEXUS must behave this way."

Instead:

> "The reference gave us a concept or principle; NEXUS business discovery determined the specific rule."

---

## Phase 0.2 Discovery Traceability

### Supplier Domain

External knowledge helped establish the distinction between:

- Supplier organization
- Supplier location/branch
- Operational contacts
- Financial relationship

NEXUS-specific discovery then determined:

- Reference Person belongs to Supplier Branch.
- Manager belongs to Supplier Branch.
- Representative belongs to Supplier Branch.
- Supplier Company owns the actual financial liability.
- Representative balances are attribution, not independent liabilities.

---

### Purchase

External domain modeling principles support treating the purchase process as a business transaction.

NEXUS discovery determined:

- Purchase Invoice = Goods Receipt.
- Original supplier invoice attachment is mandatory.
- The receiving Warehouse is explicitly selected.
- Purchase receipt produces `Download - Buy`.

---

### Supplier Return

External inventory/accounting concepts establish that returning goods can have financial and physical consequences.

NEXUS discovery determined:

- Supplier Return is represented by a Return Invoice.
- Return value may differ from original purchase value.
- Return does not automatically reduce Supplier Balance.
- The Return Invoice determines the financial settlement.
- Replacement is a separate future document.

---

### Supplier Payment

External financial transaction principles support separating a payment from invoice allocation.

NEXUS discovery determined:

- One Payment can cover multiple Purchase Invoices.
- One Payment can cover multiple Supplier Receipts.
- Payment cannot exceed amount due.
- Payment methods include Cash, Visa, Bank Transfer, and Electronic Wallet.
- Non-cash payments require evidence.
- Payment destination is explicitly recorded.

---

## Documentation Rule

Every future reference should answer:

### What did we learn?

Then:

### How did that influence NEXUS?

And finally:

### What exact NEXUS rule resulted?

This prevents external references from being incorrectly presented as requirements.

---

## Current Source Classification

### External Sources

Used to support:

- Domain Modeling
- Event Discovery
- Requirements Engineering
- Inventory Concepts
- Product Modeling
- Supply Chain Concepts

### NEXUS Business Discovery

Used to define:

- Supplier structure
- Warehouse rules
- Purchase behavior
- Stock movements
- Transfer approval flows
- Payment allocation
- Supplier Return behavior
- Representative attribution
- Business-specific terminology

---

## Principle

> **References inform the model; Business Discovery defines the NEXUS behavior.**

# NEXUS — Business Rules

> Business rules are identified during Domain Discovery.
> IDs are provisional until the Domain Map is finalized.

## Branch & Warehouse

### BR-001 — POS Branch Ownership

A POS belongs to exactly one Branch.

### BR-002 — POS Non-Transferability

A POS cannot be transferred from one Branch to another.

### BR-003 — Warehouse Branch Ownership

A Warehouse belongs to exactly one Branch.

### BR-004 — Warehouse Non-Transferability

A Warehouse cannot be transferred from one Branch to another.

---

## Users & Access

### BR-005 — Multi-Branch User

A User may operate across multiple Branches.

### BR-006 — POS Assignment

A User may operate only on POSes to which the User is assigned.

### BR-007 — Sales Eligibility

A POS assignment may specify whether the assigned User is allowed to perform sales operations.

### BR-008 — Authentication Before Access

A User must authenticate into NEXUS before accessing protected functionality.

---

## POS

### BR-009 — POS Operations

A physical POS performs Sales and Returns.

### BR-010 — POS Purchase Restriction

A physical POS does not perform Purchase operations.

### BR-011 — POS Wallet

Each POS has its own Wallet.

### BR-012 — Branch Warehouse Context

A POS operates against the Warehouse belonging to its Branch.

---

## Shift

### BR-013 — Shift Salesman

A Shift has one Salesman.

### BR-014 — Shift Managers

A Shift may have multiple Managers.

### BR-015 — Salesman Shift Exclusivity

A Salesman cannot operate on two POSes simultaneously within the same Shift context.

### BR-016 — Manager Multi-POS Participation

A Manager may participate in multiple POSes within the same Shift.

### BR-017 — Shift Continuity

A new Shift cannot start for a POS until the previous Shift has completed the required closing and confirmation process.

---

## Shift Closing

### BR-018 — Branch Settlement Confirmation

A POS-to-Branch settlement requires confirmation from a Branch Manager.

### BR-019 — Settlement Financial Effect

After confirmed settlement:

```text
POS Wallet   -X
Branch Wallet +X
```

### BR-020 — REMAIN

A Shift may end through REMAIN instead of transferring the POS balance to the Branch Wallet.

### BR-021 — REMAIN Confirmation

REMAIN requires confirmation by either the incoming Manager or incoming Salesman.

### BR-022 — REMAIN Continuity

After REMAIN confirmation, the carried amount continues into the next Shift's POS financial context.

---

## Customers

### BR-023 — Customer Grades

An existing customer has one of the following grades:

* Blocked
* Normal
* Premium
* VIP

### BR-024 — Blocked Customer

A Blocked customer cannot make a Sale until the block is removed.

### BR-025 — Takeaway Full Payment

A Takeaway Sale must be fully paid at the time of Sale.

### BR-026 — Identified Customer Remaining

An identified customer may have a Remaining amount on a Sale.

### BR-027 — Customer Receivable

A Remaining amount is recorded as a receivable/debt against the customer for the Branch.

### BR-028 — Receivable Is Not Cash

A customer receivable does not increase the Branch's physical cash balance.

---

## Payment

### BR-029 — Supported Payment Methods

Physical NEXUS currently supports:

* Cash
* Visa

### BR-030 — POS Wallet Payment Effect

The amount actually received from the customer increases the POS Wallet.

---

## Inventory

### BR-031 — Sale Inventory Effect

A completed Sale decreases the relevant Branch Warehouse stock.

### BR-032 — Return Inventory Effect

A completed Return may increase the relevant Branch Warehouse stock.

> Inventory validation and exact transaction timing remain under discovery.

---

## Deferred Domain

### BR-033 — Online Customer Scope

Online Customer operations are outside the current physical NEXUS scope.

--- 

## Product / Variant

### BR-INV-001 — Product Has a Primary Variant

Every Product must have exactly one Primary Variant.

### BR-INV-002 — Primary Variant Is Created Automatically

The Primary Variant is created automatically when the Product is created.

### BR-INV-003 — Primary Variant Is a Real Variant

The Primary Variant is a real stock-bearing Variant.

### BR-INV-004 — Product Has No Direct Stock

Stock is recorded against Product Variants, never directly against the Product.

### BR-INV-005 — Variant Stock Is Independent

Each Variant has its own Stock balance.

### BR-INV-006 — Adding a Variant Does Not Move Existing Stock

Creating a new Variant does not transfer, merge, or modify another Variant's Stock.

### BR-INV-007 — Primary Stock May Remain

The Primary Variant may continue to hold Stock after additional Variants are created.

### BR-INV-008 — Variant Cannot Add Attributes

A Variant may not introduce an Attribute that is not part of its Product's Attribute set.

### BR-INV-009 — Variant Combination Is Unique

Within a Product, the complete combination of Variant-Defining Attribute values must be unique.

### BR-INV-010 — No Automatic Combination Generation

The system does not generate every mathematically possible Variant combination.

### BR-INV-011 — User Creates Actual Variants

The User creates only the Variants actually required by the business.

### BR-INV-012 — Primary Has No Required Variant-Defining Values

The Primary Variant represents the base Product.

---

## Attribute Rules

### BR-ATTR-001 — Category Defines Base Attributes

A Category may define reusable Attribute Definitions.

### BR-ATTR-002 — Subcategory Inherits

A Subcategory inherits Category Attributes.

### BR-ATTR-003 — Subcategory May Only Add

A Subcategory may add Attributes but may not modify inherited Attribute Definitions.

### BR-ATTR-004 — Product Inherits

A Product inherits the Attribute set resulting from its classification path.

### BR-ATTR-005 — Product May Add

A Product may add Product-specific Attributes.

### BR-ATTR-006 — Lower Levels Cannot Modify Inherited Definitions

Neither Product nor Subcategory may alter the definition of an inherited Attribute.

### BR-ATTR-007 — Supported Attribute Types

TEXT, NUMBER, DATE, SELECT, MULTI_SELECT, BOOLEAN.

### BR-ATTR-008 — Any Type Can Define Variants

Any supported Attribute Type may be marked Variant-Defining.

### BR-ATTR-009 — Product Controls Allowed Values

Where an Attribute uses controlled values, the Product determines permitted values.

### BR-ATTR-010 — Variant Uses Product Values

Variant Attribute values must comply with Product Attribute definitions and constraints.

---

## Stock Rules

### BR-STK-001 — Stock Is Variant-Based

Stock is maintained per Product Variant per Warehouse.

### BR-STK-002 — Stock Is Current Physical Quantity

Stock represents the current physical quantity present in the Warehouse.

### BR-STK-003 — No Stock Status Buckets

Reserved, Damaged, Expired, and similar concepts are not modeled as Stock Detail buckets.

### BR-STK-004 — Wastage Is Separate

When Stock is lost, damaged, expired, or otherwise written off, Stock decreases and the reason is recorded separately as a future Wastage/Loss concept.

### BR-STK-005 — Stock History Is Separate From Current Balance

Future Stock Movement concepts will explain changes that produced the current Stock balance.

---

## Open Rules

- Stock Movement taxonomy.
- Wastage authorization and reasons.
- Stock Count / Adjustment reconciliation.
- Units of Measure.
- Lot/Batch/Expiry behavior.
- SKU/Barcode rules.
- Product/Variant pricing and costing.

### BR-034 — Online Warehouse Scope

The Online Customer Warehouse is deferred until the physical NEXUS domain is completed.

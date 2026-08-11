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

### BR-034 — Online Warehouse Scope

The Online Customer Warehouse is deferred until the physical NEXUS domain is completed.

---

# NEXUS — Business Rules

## Phase 0.2 Inventory Discovery — Addendum

> This section extends the existing Business Rules.
> Previous rules remain valid unless explicitly superseded.

---

## Supplier Company & Supplier Branch

### BR-SUP-001 — Supplier Company

A Supplier Company represents a company from which NEXUS purchases goods.

A Supplier Company may have multiple Supplier Branches.

---

### BR-SUP-002 — Supplier Branch

A Supplier Branch represents a specific operational branch/location of a Supplier Company.

A Supplier Branch belongs to exactly one Supplier Company.

---

### BR-SUP-003 — Branch Reference Person

A Supplier Branch has a Reference Person.

The Reference Person is associated with the Supplier Branch, not directly with the Supplier Company.

---

### BR-SUP-004 — Branch Manager

A Supplier Branch has a Manager.

The Manager is associated with the Supplier Branch, not directly with the Supplier Company.

---

### BR-SUP-005 — Branch Representative

A Supplier Branch has Supplier Representative(s).

The Representative is associated with the Supplier Branch, not directly with the Supplier Company.

---

## Supplier Balance

### BR-SUP-006 — Supplier Opening Balance

A Supplier Company may have an Opening Balance when it is introduced into NEXUS.

The Opening Balance contributes to the Supplier Company's actual financial balance.

---

### BR-SUP-007 — Representative Balance Is Attribution

A balance attributed to a Supplier Representative is not an independent financial liability.

It represents a subdivision/attribution of the Supplier Company's total financial liability.

---

### BR-SUP-008 — Representative Collection Is Transferable

A Supplier Representative other than the representative originally associated with an attributed amount may collect the amount.

The attribution does not create an independent financial liability for the Representative.

---

### BR-SUP-009 — Supplier Company Is the Actual Financial Party

The Supplier Company's financial balance represents the actual financial liability.

Branch and Representative balances are operational/attribution views of that liability unless a future rule explicitly establishes otherwise.

---

## Purchase Invoice

### BR-SUP-010 — Purchase Invoice Is Goods Receipt

Purchase Invoice and Goods Receipt represent the same business document in NEXUS.

No separate Goods Receipt document is required.

---

### BR-SUP-011 — Original Invoice Attachment Required

The original Supplier Purchase Invoice image must be attached.

The Purchase Invoice cannot be created without the required original invoice attachment.

---

### BR-SUP-012 — Purchase Invoice Warehouse

A Purchase Invoice identifies the Warehouse receiving the purchased goods.

When the Purchase Invoice is documented/approved according to the applicable workflow, the received quantity increases the selected Warehouse Stock.

---

### BR-STK-006 — Purchase Stock Movement

Purchase receipt increases Stock through:

`[ Download - Buy ]`

Reason:

`Purchase / Goods Receipt`

---

## Warehouse & Sales

### BR-STK-007 — Sales Warehouse

A Sale is fulfilled from the Main Warehouse of the Branch.

---

### BR-STK-008 — Non-Saleable Warehouses

A Secondary Warehouse or a Warehouse not associated with a Branch cannot be used directly for Sales.

---

### BR-STK-009 — Sale Stock Movement

A completed Sale decreases Stock through:

`[ Upload - Sell ]`

---

## Transfer

### BR-STK-010 — Transfer Has Two Initiation Flows

A Transfer may originate from either:

1. Destination Request → Source Approval
2. Source Order → Destination Approval

---

### BR-STK-011 — Transfer Requires Approval

A Transfer does not become an executed Stock transfer until the required approval flow is completed.

---

### BR-STK-012 — Transfer Out

The Source Warehouse decreases Stock through:

`[ Upload - Transfer ]`

---

### BR-STK-013 — Transfer In

The Destination Warehouse increases Stock through:

`[ Download - Transfer ]`

---

### BR-STK-014 — Destination Warehouse Branch Independence

The Destination Warehouse does not have to belong to a Branch.

---

### BR-STK-015 — No Reserved Quantity

NEXUS does not maintain a Reserved Quantity.

Transfer requests/orders therefore do not create a Reserved Stock bucket.

---

## Damage / Missing

### BR-STK-016 — Damage

Damaged goods decrease Stock through:

`[ Damage ]`

A predefined and stored Damage Reason must be recorded.

---

### BR-STK-017 — Missing

Missing goods decrease Stock through:

`[ Miss ]`

A predefined and stored Missing/Loss Reason must be recorded.

---

## Manual Edit

### BR-STK-018 — Manual Edit

Manual Stock Adjustment is recorded through:

`[ Manual Edit ]`

It may increase or decrease Stock.

---

### BR-STK-019 — Manual Edit Approval

A Manual Edit cannot be approved without Warehouse Manager approval.

---

## Supplier Return

### BR-SUP-013 — Supplier Return Requires a Return Invoice

Returning goods to a Supplier is represented by a Supplier Return Invoice.

It is not merely a reversal of the original Purchase Invoice.

---

### BR-SUP-014 — Supplier Return Value May Differ

The financial value of a Supplier Return may be lower than the original purchase value of the returned goods.

This is particularly relevant to goods such as expired food products.

---

### BR-STK-020 — Supplier Return Stock Movement

A Supplier Return decreases Warehouse Stock through:

`[ Upload - Supplier Returns ]`

---

### BR-SUP-015 — Return Does Not Automatically Reduce Supplier Balance

Creating a Supplier Return does not automatically reduce the Supplier Company's financial balance.

The Supplier Return Invoice determines the financial treatment.

---

### BR-SUP-016 — Return Financial Settlement

The Supplier Return Invoice may determine that the return results in a financial settlement such as:

- Cash received
- Set-off / Offset against an existing Supplier liability

Exact settlement rules remain under discovery.

---

### BR-SUP-017 — Replacement Is Separate

Supplier replacement is not part of the current Supplier Return flow.

Replacement will be represented later through a separate:

`Replacement Document`

---

## Customer Return

### BR-STK-021 — Customer Return

A Customer Return is represented by a Customer Return Invoice.

---

### BR-STK-022 — Customer Return Stock Movement

A Customer Return increases Warehouse Stock through:

`[ Download - Customer Return ]`

---

## Supplier Payment

### BR-PAY-001 — Supplier Payment Methods

Supplier Payments may be made using:

- Cash
- Visa
- Bank Transfer
- Electronic Wallet

---

### BR-PAY-002 — Non-Cash Evidence

A payment made through a non-cash method requires an image of the payment/transfer evidence.

---

### BR-PAY-003 — Payment Is Independent From One Invoice

A Supplier Payment is not restricted to a single Purchase Invoice.

---

### BR-PAY-004 — Payment Allocation

One Supplier Payment may be allocated across multiple:

- Purchase Invoices
- Supplier Receipts

---

### BR-PAY-005 — Payment Cannot Exceed Amount Due

A Supplier Payment cannot exceed the amount actually due to the Supplier.

The exact definition of "amount due" remains subject to completion of the Supplier Accounting model.

---

### BR-PAY-006 — Payment Destination

The Payment destination is explicitly recorded.

The destination may be a Supplier-related financial account/company and does not necessarily have to be the same legal/entity record represented by the Supplier Company in the Purchase Invoice.

---

## Open Rules — Updated

The following remain unresolved and must **not** be assumed:

- Stock Movement taxonomy.
- Wastage authorization and reasons.
- Stock Count / Adjustment reconciliation.
- Units of Measure.
- Lot/Batch/Expiry behavior.
- SKU/Barcode rules.
- Product/Variant pricing and costing.
- Exact Supplier Balance calculation.
- Exact Supplier Branch debt allocation behavior.
- Exact Representative allocation behavior after payment.
- Multiple-payment behavior against documents.
- Supplier Return settlement states.
- Return difference accounting/valuation.
- Replacement Document workflow.
- Supplier payment destination/account model.
- Transfer execution authority after approval.
- Damage/Miss approval requirements.
- Stock Count workflow.
- Units of Measure.
- Lot/Batch/Expiry behavior.
- SKU/Barcode rules.
- Product/Variant pricing and costing.

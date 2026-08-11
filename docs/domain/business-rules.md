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
## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

> This section extends the existing Business Rules.
> Previous rules remain preserved.
> Where a new discovery decision conflicts with an earlier provisional rule, the new decision explicitly supersedes the earlier rule without deleting historical documentation.

---

## Inventory Business Documents

### BR-STK-023 — Independent Inventory Documents

Each of the following Inventory business operations is represented by an independent business document:

- Sale
- Purchase
- Customer Return
- Supplier Return
- Transfer
- Quantity Adjustment
- Loss
- Write-off / Depreciation
- Opening Balance

A Corrective Inventory Movement generated as a consequence of an authorized document modification is not considered a separate business operation.

---

## Document Approval

### BR-STK-024 — Non-Approval Documents

The following documents do not require Approval:

- Sales
- Purchase
- Customer Return
- Supplier Return

Once saved, the document becomes Final and its Inventory Effect is applied.

---

### BR-STK-025 — Approval-Controlled Documents

The following documents require Approval before their Inventory Effect is applied:

- Transfer
- Quantity Adjustment
- Loss
- Write-off / Depreciation
- Opening Balance

---

### BR-STK-026 — Inventory Effect Timing

For documents that do not require Approval:

```text
Save
  ↓
Final
  ↓
Inventory Effect
```
For Approval-controlled documents:

```text

Save
  ↓
Pending Approval
  ↓
Approve
  ↓
Inventory Effect

```
---

## Final / Approved Documents

### BR-STK-027 — Final Document Immutability

A Final or Approved document cannot normally be modified.

---

### BR-STK-028 — Authorized Modification

A Final or Approved document may be modified only by a User having the required Permission.

---

### BR-STK-029 — Corrective Inventory Movement

When an authorized modification changes the Inventory Effect of an already-effective document:

* The original Inventory Movement remains unchanged.
* A Corrective Inventory Movement is generated.
* The resulting Stock is the effect of the original Movement plus the corrective Movement.

Example:

```text

Original Sale = 10

Original Movement = -10

Authorized correction:
10 → 8

Corrective Movement = +2

Effective Stock Effect = -8
```
--- 

### BR-STK-030 — Modification Audit

An authorized modification of a Final or Approved document must be recorded in the Approval Log.

---

## Authorization

## BR-STK-031 — Permission-Based Authorization

NEXUS Business Rules must not depend on hardcoded job titles such as:

* Manager
* Supervisor
* Director

Authorization is determined by Permissions.

A role may group Permissions, but the business capability itself is permission-based.

---

## Stock Availability
### BR-STK-032 — No Negative Stock

NEXUS must never allow Stock to become negative.

Any operation that would reduce the Stock of a Product in a Warehouse below zero must be rejected.

---
### BR-STK-033 — No Reserved Stock

NEXUS does not maintain Reserved Stock.

There is no separate Reserved Quantity.

Therefore:
```text
Available Stock = Current Stock
```
---
## Inventory Identity
### BR-STK-034 — Product and Warehouse Stock Identity

Inventory Stock is identified by:
```text
Product + Warehouse
```
Warehouse therefore affects Stock independently.

---
## BR-STK-035 — Inventory Tracking Scope

The current Inventory model does not track Stock by:

* Batch / Lot
* Serial Number
* Expiry Date

These dimensions are outside the current Inventory model.

---
## Units of Measure
### BR-STK-036 — Single Product Unit

Each Product has one Unit of Measure.

---
## BR-STK-037 — Inventory Movement Unit

Every Inventory Movement for a Product uses the Product's Unit of Measure.

NEXUS does not currently support UOM conversion or multiple Units of Measure for the same Product.

---
## Inventory Movement
### BR-STK-038 — Quantity-Only Movement

An Inventory Movement carries Quantity information only.

Cost information is not part of the Inventory Movement.

---
### BR-STK-039 — Cost Belongs to Business Documents

Invoices and business documents carry:

* Quantity
* Cost information

Inventory Movement carries:

* Quantity

This separation is intentional.

---
### Current Stock
## BR-STK-040 — Persisted Current Stock

NEXUS maintains a persisted current Stock quantity for each Product–Warehouse context.

---
## BR-STK-041 — Inventory Movement History

NEXUS records Inventory Movements as historical records explaining changes to Current Stock.

Current Stock and Inventory Movement History are both maintained.

---
## Product–Warehouse Setup
### BR-STK-042 — Product–Warehouse Setup Required

An Inventory Movement cannot be created for a Product in a Warehouse unless a Product–Warehouse Setup exists.

---
## BR-STK-043 — Automatic Product–Warehouse Setup

When a Product is added to a Warehouse, the Product–Warehouse Setup is created automatically.

The User performing the action must have the required Permission.

---
BR-STK-044 — Initial Product–Warehouse Quantity

A newly created Product–Warehouse Setup starts with Stock quantity:
```text
0
```
unless an applicable Opening Balance subsequently changes the quantity.

---
### Product–Warehouse Deactivation
## BR-STK-045 — Logical Product–Warehouse Deactivation

A Product–Warehouse Setup may be deactivated.

Deactivation is logical and does not physically delete the Setup or its historical records.

---
## BR-STK-046 — Zero Stock Required for Deactivation

A Product–Warehouse Setup cannot be deactivated while its current Stock is greater than zero.

The Stock must first be reduced to zero through valid Inventory operations.

Examples include:

* Sale
* Loss
* Write-off / Depreciation

---
### BR-STK-047 — Deactivation Has No Inventory Effect

Deactivation itself does not create an Inventory Movement.

---
## Logical Deletion
### BR-STK-048 — Logical Delete

Delete / Deactivate operations in NEXUS are logical state changes.

They do not physically remove historical business data.

---
## Transfer
### BR-STK-049 — Internal Warehouse Transfer

A Transfer is strictly:

```text
Warehouse → Warehouse
```

A Transfer cannot represent:

* Warehouse → Customer
* Warehouse → Outside the system
* Supplier → Warehouse
* Any other external inventory flow

---
### BR-STK-050 — Transfer Approval

A Transfer requires Approval before it affects Inventory.

---
### BR-STK-051 — Transfer Immediate Effect

Upon successful Approval, the Transfer immediately affects both Warehouses.
```text
Source Warehouse      -Q
Destination Warehouse +Q
```
---
### BR-STK-052 — Transfer Atomicity

A Transfer is atomic.

Either:
```text
Source -Q
Destination +Q
```
happens completely,

or:
```text
Source unchanged
Destination unchanged
```
No partially executed Transfer is allowed.

---
### BR-STK-053 — No In-Transit Inventory

NEXUS does not currently model In-Transit Inventory.

---
## Stock Reconciliation
### BR-STK-054 — Stock Reconciliation Document

Stock Reconciliation / Adjustment is represented by an independent business document.

---

## BR-STK-055 — Permission-Controlled Reconciliation

Stock Reconciliation is available only to Users having the required Permission.

---
## BR-STK-056 — Reconciliation Uses Inventory Movement

A Stock Reconciliation correction must be represented through an Inventory Movement.

The reconciliation mechanism must not bypass the Inventory Movement history.

---
## Document Attachments
### BR-DOC-001 — Attachment Requirement Configuration

Document Types may have configuration determining whether attachments are required.

The currently confirmed states are:

* Required
* Not Required

No additional attachment state is currently confirmed.

---

## Superseding Decisions
### BR-STK-057 — Transfer Approval Flow Superseded

The earlier provisional rule:
```text
Destination Request → Source Approval

OR

Source Order → Destination Approval
```

is preserved in the historical documentation but is superseded by the current discovery decision:

> A Transfer is an independent document requiring Approval, and upon Approval its Source and Destination Stock are affected atomically.
  The exact initiation-direction workflow is therefore no longer treated as a confirmed Business Rule.

---
### BR-STK-058 — Manual Edit Authorization Superseded

The earlier wording that specifically required:

> Warehouse Manager approval

is superseded by the current authorization principle:

> The required capability is determined by Permission, not by the User's job title.

---
## Open Rules — Checkpoint 0.2-A

The following remain unresolved:

Exact Customer Return rules.
Exact Supplier Return rules.
Whether Returns require reference to an original document.
Partial Return behavior.
Opening Balance recurrence rules.
Exact Quantity Adjustment semantics.
Adjustment reason requirements.
Exact distinction between Loss and Write-off / Depreciation.
Detailed Stock Reconciliation behavior.
Approval Log structure and required fields.
Exact validation timing for multi-line documents.

# NEXUS — Requirements Discovery

> This document represents the current discovery state.
> It is not a final technical specification.

## 1. Functional Areas

NEXUS currently contains the following functional areas:

* Authentication
* Authorization
* Branch Management
* POS Management
* POS Assignment
* Warehouse / Inventory
* Sales
* Returns
* Shifts
* POS Wallet
* Branch Wallet
* Customers
* Customer Grades
* Customer Receivables

---

## 2. Authentication

Users must authenticate into NEXUS before accessing protected functionality.

The user's role and permissions determine the available functionality.

---

## 3. POS Access

A user may be assigned to one or more POSes.

A POS assignment may determine whether the user can perform sales operations.

A Salesman must select an assigned POS before beginning POS sales operations.

---

## 4. Sales

The physical POS supports:

* Sales
* Returns

The physical POS does not support:

* Purchase operations

---

## 5. Customers

The physical sales process supports:

* Takeaway customers
* Existing/identified customers
* Registration of a new customer during the sales flow

Customers have grades:

* Blocked
* Normal
* Premium
* VIP

Blocked customers cannot be sold to until the block is removed.

---

## 6. Payment

Supported payment methods:

* Cash
* Visa

Takeaway sales require full payment.

Identified customers may have a remaining balance.

---

## 7. Receivables

A remaining amount on an identified customer's Sale is recorded as a customer receivable/debt for the Branch.

The receivable is not treated as cash received into the Branch Wallet.

---

## 8. Inventory

Sales reduce stock in the relevant Branch Warehouse.

Returns can increase stock in the relevant Branch Warehouse.

The exact stock validation, reservation, deduction timing, and failure behavior remain open discovery topics.

---

## 9. Shift Management

A POS may have multiple Shifts over time.

A new Shift cannot start before the previous Shift has completed the required closing/confirmation process.

A Shift includes:

* One Salesman
* One or more Managers

A Salesman cannot operate two POSes simultaneously within the same Shift context.

A Manager may participate in multiple POSes within the same Shift.

---

## 10. Shift Closing

A Shift may close through:

### Settlement

Transfer the POS financial balance to the Branch Wallet.

Requires Branch Manager confirmation.

### REMAIN

Carry the POS balance into the next Shift.

Requires confirmation by either the incoming Manager or Salesman.

---

## 11. Open Requirements

The following are intentionally unresolved:

* Exact inventory availability behavior.
* Whether stock is checked at product selection, payment, or completion.
* Behavior when requested quantity exceeds available stock.
* Exact Sale completion state transitions.
* Exact Return workflow.
* Return authorization rules.
* Customer registration fields.
* Customer blocking/unblocking authority.
* Exact accounting representation of receivables.
* Exact Wallet transaction model.
* Exact Shift state machine.
* Manager assignment rules.

---

## Phase 0.2 — Inventory Requirements

### Product / Variant

- Every Product has exactly one Primary Variant.
- The Primary Variant is created automatically with the Product.
- The Primary Variant is a real Variant and can hold Stock.
- Product has no independent Stock balance.
- Each Variant has an independent Stock balance.
- A Variant cannot introduce an Attribute outside the Product Attribute set.
- Variant identity is based on the complete combination of Variant-Defining Attribute values.
- Duplicate Variant-defining combinations are not allowed within the same Product.
- The system does not auto-generate every possible Variant combination.
- The User creates only the Variants actually needed.
- The Primary Variant is the base Product representation.

### Attributes

Current Attribute Types:

- TEXT
- NUMBER
- DATE
- SELECT
- MULTI_SELECT
- BOOLEAN

Rules:

- Category defines reusable Attribute Definitions.
- Subcategory inherits and may add Attributes.
- Product inherits and may add Product-specific Attributes.
- Variants may only use Product Attributes.
- Any supported Attribute Type may be Variant-Defining.

### Stock

- Stock is the current physical quantity of a Product Variant in a Warehouse.
- Stock is not divided into Reserved/Damaged/Expired status buckets.
- Reserved is explicitly out of the current Inventory model.
- Damaged/Expired are not Stock Details.
- Wastage/Loss reduces current Stock.
- Stock history will be represented through future Stock Movement concepts.

### Additional Open Questions

- What exact Stock Movement types exist?
- How is Wastage/Loss authorized?
- Which Wastage reasons are configurable?
- Are Stock Counts/Adjustments required?
- What Unit of Measure rules apply?
- Are Lot/Batch/Expiry attributes required?
- How will SKU/Barcode work?
- How do pricing and costing relate to Product vs Variant?

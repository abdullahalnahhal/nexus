# NEXUS — Business Rules

## Inventory Foundation

### BR-INV-001 — Current Stock Source of Truth

`Current Stock` is the Source of Truth for the current inventory quantity.

### BR-INV-002 — Current Stock Uniqueness

For every `Product + Warehouse`, NEXUS maintains exactly one Current Stock record.

### BR-INV-003 — Product-Warehouse Identity

Warehouse affects inventory identity. Batch/Lot, Serial Number, Expiry Date, and Unit of Measure do not affect inventory identity in the current phase.

### BR-INV-004 — No Negative Stock

Inventory quantity cannot become negative.

### BR-INV-005 — No Reserved Stock

NEXUS currently has no separate Reserved Stock / Stock Reservation quantity.

### BR-INV-006 — Product Unit

Every Product has a single Unit in the current phase.

### BR-INV-007 — Product-Warehouse Setup

A Product-Warehouse Setup is required before inventory movements. Adding a Product to a Warehouse automatically creates its Product-Warehouse Setup. A Product-Warehouse Setup may be deactivated only after its stock has been cleared.

### BR-INV-008 — Stock Movement Meaning

Stock Movement represents the inventory effect of an Inventory Document. It carries Quantity and direction (`IN` or `OUT`).

### BR-INV-009 — Stock Movement Immutability

A Stock Movement is immutable after creation. It cannot be edited or deleted as a means of correcting inventory. Corrections must be represented by an appropriate Inventory Document that produces a new Stock Movement.

### BR-INV-010 — Document-to-Movement Relationship

An Inventory Document may produce one or more Stock Movements. A Stock Movement references the Inventory Document that caused it.

### BR-INV-011 — Current Stock Mutation

Stock Movement applies its inventory effect to the corresponding Current Stock record. Normal user flows do not directly edit Current Stock.

### BR-INV-012 — Transfer Atomicity

A Warehouse-to-Warehouse Transfer produces an OUT movement at the source and an IN movement at the destination. Both effects succeed together or neither is applied.

### BR-INV-013 — Movement Quantity vs Cost

Stock Movement carries Quantity only. Invoices/documents carry Quantity + Cost where applicable.

### BR-INV-014 — Inventory Documents

The established inventory operations are:

1. Sale
2. Purchase
3. Customer Return
4. Supplier Return
5. Transfer Warehouse-to-Warehouse
6. Quantity Adjustment
7. Loss
8. Depreciation
9. Opening Balance

### BR-INV-015 — Approval

Sales, Purchase, Customer Return, and Supplier Return do not require approval. Other established inventory operations require approval.

### BR-INV-016 — Finality

An invoice once saved is final. After Approval, a document is non-editable unless the user has the required permission and the established approval/audit mechanism permits the action.

### BR-INV-017 — Authorization

Authorization is permission-based. `Manager` is not a hardcoded authorization concept. Stock Reconciliation / Adjustment availability and actions depend on permissions.

### BR-INV-018 — Stock Reconciliation / Adjustment

Stock Reconciliation / Adjustment is a separate document and does not imply a direct edit of Current Stock.

### BR-INV-019 — No Accounting Effect for Stock Adjustment

Stock Adjustment/Reconciliation does not inherently require an accounting effect.

## Related Established Rules

### BR-INV-020 — Purchase Invoice

Purchase Invoice is the Goods Receipt.

### BR-INV-021 — Supplier Return

A Supplier Return may have a value different from the original purchase value. The return document determines whether the amount is received as cash or offset.

### BR-INV-022 — Customer Return

The current phase treats a customer return as a return invoice without replacement. Replacement is represented as a separate replacement document and is not part of the current return scope.

### BR-INV-023 — Transfer Destination

A destination Warehouse for a transfer should not be tied to a Branch.

### BR-INV-024 — Transfer Scope

Transfers occur between Warehouses only.

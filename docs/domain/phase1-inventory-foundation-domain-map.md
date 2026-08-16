# NEXUS — Domain Map

## Inventory Boundary

The inventory model distinguishes three concepts.

### 1. Inventory Document

Represents the business transaction and its business meaning.

Examples:

- Sale
- Purchase
- Customer Return
- Supplier Return
- Warehouse Transfer
- Quantity Adjustment
- Loss
- Depreciation
- Opening Balance

The document owns the business transaction data, lifecycle, approval where applicable, and references/attachments according to the established rules.

### 2. Stock Movement

Represents the inventory effect produced by an Inventory Document.

A Stock Movement records quantity movement for a specific:

- Product
- Warehouse

The movement has a direction:

- `IN`
- `OUT`

A Stock Movement is not an Inventory Document and is not a copy of one.

Stock Movement is immutable after creation.

### 3. Current Stock

Represents the current inventory state for a specific:

`Product + Warehouse`

There is exactly one Current Stock record for each Product + Warehouse.

`Current Stock` is the Source of Truth for current inventory quantity.

## Relationship

```text
Inventory Document
        |
        | produces
        v
Stock Movement
        |
        | applies
        v
Current Stock
```

The Stock Movement keeps a reference to its originating Inventory Document.

## Transfer

A warehouse-to-warehouse Transfer is one business document but produces two inventory effects:

```text
Transfer Document
       |
       +-- OUT Movement --> Source Warehouse Current Stock
       |
       +-- IN Movement  --> Destination Warehouse Current Stock
```

The two movements are atomic: both are applied together, or neither Current Stock record changes.

## Important Boundary Rules

- A normal inventory quantity change originates from an Inventory Document.
- Stock Movement is not a user-editable Current Stock adjustment.
- Current Stock is not a historical ledger.
- Stock Movement is not the Source of Truth for the current quantity.
- Current Stock is not derived conceptually as a replacement for Stock Movement.
- Cost belongs to invoice/document data in the current phase; Stock Movement carries Quantity only.
- Batch/Lot, Serial Number, Expiry Date, and Unit of Measure do not affect inventory identity in the current phase.
- Negative stock is not allowed.
- There is currently no Reserved Stock model.

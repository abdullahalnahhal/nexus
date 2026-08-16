# NEXUS — Phase 1: Inventory Foundation

## Status

**Current checkpoint:** Inventory Foundation / Domain Boundaries

## Established Inventory Model

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

## Current Stock

- Source of Truth for current inventory quantity.
- Exactly one record for each Product + Warehouse.
- Cannot be negative.
- Not a historical ledger.
- Not directly edited by normal user flows.

## Stock Movement

- Inventory effect produced by an Inventory Document.
- Identified by Product + Warehouse.
- Carries Quantity only in the current phase.
- Direction is IN or OUT.
- Immutable after creation.
- References its originating Inventory Document.
- Applies its effect to Current Stock.
- Does not replace Current Stock as the source of current quantity.

## Inventory Document

- Represents the business transaction.
- May produce one or more Stock Movements.
- Owns business-level information such as parties, dates, lifecycle, approval, attachments, quantities, and costs where applicable.
- Is the business origin of the inventory effect.

## Transfer

A Transfer Document creates:

- one OUT Movement for the source warehouse;
- one IN Movement for the destination warehouse.

The two effects are atomic.

## Scope of Inventory Identity

Current identity is:

`Product + Warehouse`

Not currently part of identity:

- Batch/Lot
- Serial Number
- Expiry Date
- Unit of Measure

## Current Inventory Operations

1. Sale
2. Purchase
3. Customer Return
4. Supplier Return
5. Transfer Warehouse-to-Warehouse
6. Quantity Adjustment
7. Loss
8. Depreciation
9. Opening Balance

## Lifecycle

Applicable documents follow the already-established finality and approval rules.

Stock Movement is created only as the inventory effect of the applicable document lifecycle.

Once created, Stock Movement is immutable.

## Explicit Non-Goals for This Checkpoint

The following are not being introduced:

- Reserved Stock
- negative stock
- stock details as a separate source of truth
- cost on Stock Movement
- batch/serial/expiry-based inventory identity
- direct user editing of Current Stock
- Event Sourcing as an architectural commitment
- a hardcoded Manager authorization model

## Next Boundary Questions

The next design work should build on these decisions rather than rediscover them. Potential next questions include:

- exact lifecycle point at which a document produces its movement(s);
- aggregate/transaction boundaries;
- persistence constraints enforcing one Current Stock per Product + Warehouse;
- movement/document references;
- reversal/correction patterns built on immutable movements.

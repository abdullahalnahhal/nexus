# NEXUS — Stock Adjustment Domain Addendum

## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

This addendum extends the existing Domain Map without replacing prior decisions.

### Stock Adjustment

```text
Stock Adjustment
├── Warehouse Context
├── Adjustment Reason / Originating Reference
├── Product Lines
├── Permission-controlled Issuance
└── Immediate Inventory Effect
```

### Domain Rules

- Stock Adjustment is a business document representing a justified inventory quantity change.
- The adjustment must carry an allowed reason and/or originating reference for traceability.
- A user may create it manually when the relevant Permission is granted and the reason is allowed.
- Issuance immediately mutates current stock.
- The same Product may occur on multiple lines; the inventory effect is based on the aggregate quantity for that Product within the document.
- An issued Stock Adjustment is immutable and cannot be cancelled.
- Stock Adjustment has no accounting effect in the current scope.
- UOM behavior remains deferred.

### Authorization correction

The earlier generic Domain Map described Adjustment among approval-controlled inventory documents. For **Stock Adjustment specifically**, Phase 0.2 now establishes that an additional approval step is not required: the required Permission is sufficient for direct issuance.

This addendum supersedes only that generic assumption for Stock Adjustment and does not alter approval rules for other inventory documents.

# NEXUS — Supplier Return Business Rules Addendum

> Phase 0.2 Inventory Discovery.
> Append-only addendum. Existing Business Rules history remains unchanged.

## BR-SR-001 — Purchase Invoice Is Optional

Supplier Return does not require a Purchase Invoice.

If a Purchase Invoice exists, its reference may be stored on the Supplier Return as optional data.

## BR-SR-002 — Permission-Based Operation

Creating/issuing a Supplier Return is authorized through permissions assigned to the user responsible for the Warehouse operation.

No hardcoded role is required by this rule.

## BR-SR-003 — Required Invoice Data

Supplier Return Invoice issuance requires:

- Supplier.
- Representative.
- Items.
- Quantity per item.
- Total Invoice Amount.
- Attachments.

## BR-SR-004 — Optional Item Return Price

A return price may be entered for an individual item, but it is optional.

The absence of item-level return prices does not prevent Supplier Return Invoice issuance.

## BR-SR-005 — Explicit Total Invoice Amount

The Supplier Return Invoice has an explicitly specified total amount.

The invoice is issued for that total amount; it is not required to be calculated from optional item-level return prices.

## BR-SR-006 — Return Warehouse Required

A Supplier Return must identify the Warehouse from which the goods are returned.

The responsible user must have permission to operate on the selected Warehouse.

## BR-SR-007 — Available Stock Constraint

The aggregate quantity being returned for a Product must not exceed that Product's available stock in the selected Warehouse.

```text
Aggregate Return Qty <= Available Stock
```

## BR-SR-008 — Immediate Stock Deduction

Issuing a Supplier Return immediately deducts the returned quantities from the selected Warehouse stock.

Financial settlement timing does not delay this inventory effect.

## BR-SR-009 — Repeated Product Lines Are Aggregated

If the same Product appears on multiple Supplier Return lines, the inventory effect is based on the aggregate quantity of those lines.

## BR-SR-010 — Supplier-Defined Settlement Method

The Supplier Return does not impose a single financial settlement method.

The actual agreed method may include debt/payable reduction, cash, bank transfer, or another supported method.

The selected method and actual settled amount must be recorded.

Supporting settlement files/attachments must also be recorded.

## BR-SR-011 — Immediate or Deferred Settlement

The Supplier Return Invoice allows the financial settlement timing to be selected as:

- Immediate settlement.
- Deferred settlement.

Stock is deducted immediately in both cases.

## BR-SR-012 — Deferred Settlement

When deferred settlement is selected, the Supplier Return may be issued and stock deducted before the Supplier actually performs the financial settlement.

The later actual settlement must be recorded when it occurs.

## BR-SR-013 — No Customer Return Settlement Symmetry

Supplier Return settlement rules are independent from Customer Return settlement rules.

Supplier Return currently permits flexible settlement timing and method based on the Supplier agreement.

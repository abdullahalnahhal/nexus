# NEXUS — Customer Return Discovery

> Phase 0.2 Inventory Discovery — Checkpoint 0.2-B onward.
> This document is an append-only discovery record for Customer Return.
> It does not replace earlier Business Rules or Domain Map history.

## Status

**Customer Return discovery decisions captured through Checkpoint 0.2-D.**

## 1. Original Sales Invoice Reference

A Customer Return **must** reference an existing Sales Invoice.

A Customer Return cannot be created without an original Sales Invoice reference.

A Cancelled / Voided Sales Invoice is not available for selection from the POS and therefore cannot be used as the source of a Customer Return.

## 2. Return-to-Invoice Relationship

One Customer Return references exactly **one Sales Invoice**.

A Sales Invoice may have multiple Customer Returns.

A single Customer Return cannot combine lines from multiple Sales Invoices.

If a customer returns goods originating from multiple Sales Invoices, a separate Customer Return is created for each Sales Invoice.

Example:

```text
Sales Invoice #SI-001
    └── Customer Return #CR-001

Sales Invoice #SI-002
    └── Customer Return #CR-002

Sales Invoice #SI-003
    └── Customer Return #CR-003
```

## 3. Returned Item Eligibility

A Customer Return may contain only products/items that exist on its referenced Sales Invoice.

If an item has no Sales Invoice from which it was sold to the customer, it cannot be returned through Customer Return.

## 4. Original Sales Price

The Customer Return uses the price recorded on the corresponding original Sales Invoice line.

The return price is not entered independently and does not use the current product price.

Discounts and taxes are explicitly outside the scope of the current discovery stage.

## 5. Returnable Quantity

The total quantity returned for a Sales Invoice line cannot exceed the quantity originally sold on that line.

Because a Sales Invoice may have multiple Customer Returns, the constraint applies to the aggregate of all Customer Returns associated with the original Sales Invoice line.

```text
Remaining Returnable Qty =
    Original Sold Qty
    - Total Previously Returned Qty
```

The total returned quantity must never exceed the original sold quantity.

### Multiple Returns Example

```text
Sales Invoice #SI-001
Product A
Sold Qty = 10

Customer Return #CR-001
Returned Qty = 4

Customer Return #CR-002
Returned Qty = 3

Remaining Returnable Qty = 3
```

A further return of 4 units is not allowed.

## 6. Same Product on Multiple Return Lines

A Customer Return may contain the same Product more than once, provided that the applicable aggregate returned quantity remains within the original quantity sold.

## 7. Return Splitting Policy

Sales UOM behavior and Return Splitting behavior are separate concepts.

A UOM may allow fractional quantities during Sales while the corresponding Sales Invoice line may still require a full-line return.

NEXUS therefore models a **Return Splitting Policy** independently from the Sales UOM.

The policy may be:

- `Partial Return Allowed`
- `Full Line Return Only`

### Partial Return Allowed

A line such as:

```text
Product A
Original Qty: 10 Kg
```

may be returned in multiple partial returns, provided the aggregate returned quantity does not exceed 10 Kg.

### Full Line Return Only

A line such as:

```text
Product B
Original Qty: 2.750 Kg
Return Splitting Policy: Full Line Return Only
```

must be returned as the complete original line quantity if it is returned at all.

Allowed:

```text
Return: 2.750 Kg
```

Not allowed:

```text
Return: 2.000 Kg
Return: 1.500 Kg
Return: 0.750 Kg
```

This rule applies **only to Return behavior**. It does not mean that the Sales UOM cannot be fractional during Sales.

## 8. POS Returnable Quantity Presentation

When a Sales Invoice is selected for Customer Return from the POS, the POS displays only quantities that are still eligible for return.

For each eligible line, the POS displays:

- Original sold quantity.
- Remaining returnable quantity.
- A link to view previous return operations for the line.

Example:

```text
Product A
Original Qty:        10
Previously Returned:  6
Remaining:            4
[View Returns]
```

The POS must not allow the user to enter a quantity greater than the remaining returnable quantity.

When the remaining quantity reaches zero, the line is no longer eligible for return from that Sales Invoice.

The POS behavior is therefore a presentation of the same business rule; it does not replace server-side validation.

## 9. Return Warehouse

The Warehouse receiving the returned goods does not have to be the same Warehouse from which the original Sales Invoice was fulfilled.

Example:

```text
Original Sale:
Warehouse A → Customer

Customer Return:
Customer → Warehouse B
```

The Return Warehouse is operationally independent from the original Sales Warehouse.

## 10. Immediate Inventory and Financial Effect

Customer Return settlement is performed immediately when the Customer Return Invoice is created.

Both effects are immediate:

- Inventory effect.
- Financial settlement effect.

There is no deferred financial settlement for the current Customer Return flow.

## 11. Full Financial Settlement

The Customer Return value must be fully settled at the time the Customer Return is created.

Partial settlement is not supported in the current flow.

## 12. Cash Refund

Cash is the supported Customer Return refund method in the current phase.

## 13. Customer Debt Settlement

If the customer has outstanding debt, the Customer Return amount is first deducted from the customer's **total outstanding debt**.

The debt is not restricted to the Sales Invoice from which the returned goods originated.

If the return amount exceeds the customer's outstanding debt, the remaining amount is returned to the customer in cash.

Examples:

```text
Return Amount = 1,000
Customer Debt = 0

Debt Settlement = 0
Cash Refund = 1,000
```

```text
Return Amount = 1,000
Customer Debt = 3,000

Debt Settlement = 1,000
Cash Refund = 0
Remaining Debt = 2,000
```

```text
Return Amount = 1,000
Customer Debt = 600

Debt Settlement = 600
Cash Refund = 400
Remaining Debt = 0
```

## 14. Accounting Treatment — Current Scope

No Accounting Journal Entries are created by Customer Return in the current discovery scope.

The Customer Return financial behavior is limited to the immediate customer settlement described above.

## 15. Return Period

The allowed Customer Return period is configurable through Return Settings.

It is not hardcoded as a fixed Business Rule at this stage.

## 16. Customer Return Cancellation

A Customer Return cannot be cancelled after creation.

There is no Customer Return cancellation/reversal flow in the current model.

Correction through a separate Sales transaction remains a future business-flow topic and is not further defined by this document.

## 17. Explicitly Out of Current Scope

The current Customer Return discovery does not define:

- Taxes.
- Discounts.
- Accounting Journal Entries.
- Multiple UOM conversion.
- Batch / Lot / Serial / Expiry tracking.

## 18. Open Customer Return Questions

The following are intentionally left open for later discovery:

- Exact configuration scope and ownership of Return Splitting Policy.
- Exact behavior when a Sales Invoice is outside the configured Return Period.
- Detailed behavior of the separate Sales transaction used for any future correction scenario.
- Any additional POS workflow constraints not yet discovered.

# NEXUS — Customer Return Business Rules Addendum

> Phase 0.2 Inventory Discovery — Customer Return.
> Append-only addendum. Existing Business Rules remain preserved.

## Customer Return Reference

### BR-CR-001 — Sales Invoice Reference Required

A Customer Return must reference an existing Sales Invoice.

A Cancelled / Voided Sales Invoice is not selectable from the POS and therefore cannot be returned.

### BR-CR-002 — One Return References One Sales Invoice

A Customer Return references exactly one Sales Invoice.

A Sales Invoice may have multiple Customer Returns.

A Customer Return cannot combine lines from multiple Sales Invoices.

### BR-CR-003 — Returned Item Must Exist on Referenced Invoice

Every item returned through a Customer Return must exist on the referenced Sales Invoice.

An item with no applicable Sales Invoice cannot be returned through Customer Return.

### BR-CR-004 — Original Sales Price

The Customer Return uses the price recorded on the corresponding original Sales Invoice line.

The current product price or an independently entered return price is not used.

Discounts and taxes are outside the current discovery scope.

## Quantity Rules

### BR-CR-005 — Aggregate Return Quantity Limit

The total quantity returned for a Sales Invoice line cannot exceed the quantity originally sold on that line.

For multiple Customer Returns, the remaining returnable quantity is:

```text
Remaining Returnable Qty =
    Original Sold Qty
    - Total Previously Returned Qty
```

### BR-CR-006 — Same Product May Appear More Than Once

A Customer Return may contain the same Product more than once, provided the aggregate returned quantity remains within the original sold quantity.

### BR-CR-007 — Return Splitting Policy

Return Splitting Policy is independent from Sales UOM behavior.

The current policies are:

- Partial Return Allowed
- Full Line Return Only

Sales may use fractional quantities even when the corresponding Sales Invoice line is configured as Full Line Return Only.

### BR-CR-008 — Full Line Return

When a Sales Invoice line uses `Full Line Return Only`, the line must be returned using its complete original quantity if it is returned at all.

The line cannot be partially returned.

## POS Behavior

### BR-CR-009 — Show Remaining Returnable Quantity

When a Sales Invoice is selected in the POS for Customer Return, the POS shows only quantities still eligible for return.

For each eligible line, the POS shows:

- Original sold quantity.
- Remaining returnable quantity.
- A link to view previous return operations.

The POS must not permit entry of a quantity greater than the remaining returnable quantity.

When remaining quantity reaches zero, the line is no longer eligible for return.

## Warehouse

### BR-CR-010 — Independent Return Warehouse

The Warehouse receiving returned goods may differ from the Warehouse that fulfilled the original Sales Invoice.

## Timing and Settlement

### BR-CR-011 — Immediate Effects

Creating a Customer Return immediately applies:

- The Inventory effect.
- The financial settlement effect.

### BR-CR-012 — Full Settlement Required

The Customer Return amount must be fully settled when the Customer Return is created.

Partial settlement is not supported.

### BR-CR-013 — Cash Refund

Cash is the supported Customer Return refund method in the current phase.

### BR-CR-014 — Settle Customer Debt First

If the customer has outstanding debt, the Customer Return amount is first deducted from the customer's total outstanding debt.

If the return amount exceeds the customer's total outstanding debt, the remaining amount is returned to the customer in cash.

### BR-CR-015 — No Return Journal Entries

Customer Return does not create Accounting Journal Entries in the current discovery scope.

## Configuration and Lifecycle

### BR-CR-016 — Configurable Return Period

The permitted Customer Return period is configurable through Return Settings.

### BR-CR-017 — Customer Return Cannot Be Cancelled

A Customer Return cannot be cancelled after creation.

There is no Customer Return cancellation/reversal flow in the current model.

## Current Scope Exclusions

The Customer Return discovery currently excludes:

- Taxes.
- Discounts.
- Accounting Journal Entries.
- UOM conversion.
- Batch / Lot / Serial / Expiry tracking.

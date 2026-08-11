# NEXUS — Supplier Return Discovery

> Phase 0.2 Inventory Discovery — Supplier Return.
> This document is an append-only discovery record for Supplier Return.
> It does not replace earlier Business Rules or Domain Map history.

## Status

**Supplier Return discovery decisions captured through the current Inventory Discovery checkpoint.**

## 1. Supplier Return Is an Independent Document

A Supplier Return is an independent return document.

A Purchase Invoice is **not required** in order to create or issue a Supplier Return.

The existence of a Purchase Invoice does not define whether the return is valid.

## 2. Optional Purchase Invoice Reference

If a Purchase Invoice exists and is relevant to the Supplier Return, it may be recorded as reference/data on the Supplier Return.

The Purchase Invoice reference is optional.

It is not the source from which the Supplier Return's supplier, items, quantities, or prices must be derived.

## 3. Authorization

The Supplier Return operation is performed by the responsible Warehouse user/process, subject to the user's configured permissions.

Authorization is permission-based and does not depend on a hardcoded role such as `Warehouse Manager`.

## 4. Required Supplier Return Invoice Data

The following data is required to issue a Supplier Return Invoice:

- Supplier.
- Representative.
- Items.
- Quantity for each item.
- Total Invoice Amount.
- Attachments.

These values are entered as part of the Supplier Return operation rather than being required to come from a Purchase Invoice.

## 5. Optional Supplier Return Data

The following are optional:

- Return price for an individual item.
- Purchase Invoice reference.

A Supplier Return Invoice remains valid and issuable when item-level return prices are not provided.

## 6. Total Invoice Amount

The Supplier Return Invoice has an explicitly specified **Total Invoice Amount**.

The total invoice amount is not required to be derived from item-level return prices because item-level return prices are optional.

The Supplier Return Invoice cannot be issued with a different total from the total amount specified for the invoice itself.

## 7. Return Warehouse

The Warehouse from which the goods are returned must be explicitly selected.

The selected Warehouse must be one that the responsible user is authorized to operate on through permissions.

## 8. Stock Availability

Every returned quantity must be available in the selected return Warehouse.

The Supplier Return must not allow the requested return quantity to exceed the Warehouse's available stock.

```text
Requested Return Qty <= Available Stock
```

This validation applies to the aggregate quantity of the same Product being returned from the same Warehouse.

## 9. Immediate Inventory Effect

The Supplier Return reduces stock **immediately when the Supplier Return Invoice is issued**.

Financial settlement timing does not delay the inventory effect.

```text
Issue Supplier Return
        |
        +--> Stock deducted immediately
        |
        +--> Financial settlement: immediate OR deferred
```

## 10. Repeated Product Lines

A Supplier Return may contain the same Product more than once.

For inventory purposes, repeated lines for the same Product are aggregated when determining the quantity to deduct.

Example:

```text
Product X
Line 1: 3
Line 2: 2

Total stock deduction = 5
```

The aggregate quantity must still be within the available stock of the selected Warehouse.

## 11. Financial Refund / Settlement

The financial return from the Supplier is not constrained to one fixed settlement method.

The Supplier determines the agreed refund/settlement form. Examples include:

- Reduction of the amount owed to the Supplier.
- Cash.
- Bank transfer.
- Another supported settlement method.

The selected settlement method and the amount actually settled must be recorded.

Supporting settlement files/attachments must also be recorded.

The actual settlement amount **may differ from the Supplier Return Invoice Total Amount**.

A Supplier Return may have **more than one financial settlement record** over its lifecycle.

A settlement may be **partial**. Therefore, the total of recorded settlement amounts may remain below the Supplier Return Invoice Total Amount, leaving an outstanding/unsettled amount.

The Supplier Return Invoice amount represents the return document's declared total; it is not a hard constraint on the amount(s) subsequently settled by the Supplier.

## 12. Settlement Timing

The Supplier Return Invoice supports both settlement timings:

### Immediate Settlement

The financial refund/settlement is recorded as part of issuing the Supplier Return.

Immediate settlement does not require the settlement amount to equal the Supplier Return Invoice Total Amount and may be partial.

### Deferred Settlement

The Supplier Return is issued first and the inventory is reduced immediately, while the financial refund/settlement is recorded later when the Supplier actually performs the agreed settlement.

Deferred settlement may result in one or more later settlement records, including partial settlements.

The choice between Immediate and Deferred Settlement is available on the Supplier Return Invoice itself.

## 13. Supplier Settlement Is Not Forced Into Customer Return Rules

Supplier Return settlement is intentionally different from Customer Return settlement.

Customer Return currently requires immediate full settlement using the current Cash refund flow.

Supplier Return allows the settlement timing and settlement method to vary according to the agreement with the Supplier, while recording the actual settlement data and supporting files.

## 14. Supplier Return Lifecycle

The current discovered lifecycle is:

```text
Authorized Warehouse User
        |
        v
Create Supplier Return Invoice
        |
        +--> Supplier
        +--> Representative
        +--> Warehouse
        +--> Items
        +--> Quantities
        +--> Total Invoice Amount
        +--> Required Attachments
        +--> Optional Purchase Invoice Reference
        +--> Optional Item Return Prices
        +--> Settlement Timing
                |
                +--> Immediate
                |      |
                |      +--> Issue Return
                |      +--> Deduct Stock Immediately
                |      +--> Record zero, one, or more applicable settlement records
                |      +--> Settlement may be partial
                |
                +--> Deferred
                       |
                       +--> Issue Return
                       +--> Deduct Stock Immediately
                       +--> Later record one or more actual Supplier Settlement records
                       +--> Each settlement may be partial
```

## 15. Explicitly Decided Constraints

The Supplier Return:

- Does not require a Purchase Invoice.
- Does require an explicitly selected Supplier.
- Does require an explicitly selected Representative.
- Does require an explicitly selected return Warehouse.
- Does require item quantities.
- Does require the Total Invoice Amount.
- Does require Attachments for issuance.
- May optionally reference a Purchase Invoice.
- May optionally contain item-level return prices.
- Cannot return more than the available stock in the selected Warehouse.
- Deducts stock immediately on issuance.
- May contain the same Product on multiple lines; stock deduction uses the aggregate quantity.
- Supports immediate or deferred financial settlement.
- Supports multiple financial settlement records over the Supplier Return lifecycle.
- Supports partial financial settlement.
- Does not require settlement amount(s) to equal the Supplier Return Invoice Total Amount.
- Supports supplier-defined settlement methods, which must be recorded with supporting files.

## 16. Still Open — Points Not Yet Decided

The following are intentionally not assumed by this document:

- Whether a deferred settlement has a dedicated status/lifecycle before the actual settlement is recorded.
- The exact supported list and configuration model for settlement methods.
- The exact accounting treatment of Supplier Return and Supplier settlement.
- Whether a Supplier Return can be corrected after issuance, since stock is already affected immediately.
- Any future rules around taxes, discounts, UOM conversion, batches/lots/serials, or expiry tracking.

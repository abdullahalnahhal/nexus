# NEXUS — Customer Return Domain Addendum

> Phase 0.2 Inventory Discovery — Customer Return.
> Append-only Domain Map addendum. Existing Domain Map history remains preserved.

## Customer Return Domain Shape

```text
Sales Invoice
     │
     │ 1
     ▼
Customer Return
     │
     ├── Customer
     ├── Returned Items / Lines
     ├── Return Warehouse
     ├── Original Sales Price
     ├── Return Splitting Policy
     ├── Inventory Effect
     └── Immediate Financial Settlement
```

## Invoice Relationship

```text
Sales Invoice #SI-001
       │
       ├── Customer Return #CR-001
       ├── Customer Return #CR-002
       └── Customer Return #CR-003
```

A Customer Return references exactly one Sales Invoice.

A Sales Invoice may have multiple Customer Returns.

A Customer Return does not combine lines from multiple Sales Invoices.

## Returnable Line

A Customer Return line is derived from an eligible original Sales Invoice line.

```text
Original Sales Invoice Line
       │
       ├── Product
       ├── Original Quantity
       ├── Original Price
       └── Return Splitting Policy
                │
                ▼
       Customer Return Line
```

The aggregate returned quantity cannot exceed the original sold quantity.

## Return Splitting Policy

Return Splitting Policy is independent from Sales UOM.

```text
Return Splitting Policy
        │
        ├── Partial Return Allowed
        │
        └── Full Line Return Only
```

A Sales UOM may support fractional quantities during Sales while the Return Splitting Policy may require the complete original line quantity on Return.

For `Full Line Return Only`, a weighted line such as `2.750 Kg` is returned as `2.750 Kg` or not returned; it is not partially returned.

## Return Warehouse

```text
Original Sales
Warehouse A ─────► Customer

Customer Return
Customer ─────► Warehouse B
```

The Return Warehouse is independent from the original Sales Warehouse.

## POS Return View

When a Sales Invoice is selected in the POS:

```text
Sales Invoice Line
       │
       ├── Original Qty
       ├── Previously Returned Qty
       ├── Remaining Returnable Qty
       └── View Previous Returns
```

Only eligible remaining quantities are presented for return.

When remaining quantity is zero, the line is not eligible for another return.

## Immediate Effects

```text
Customer Return Invoice
          │
          ├──────────────► Inventory Effect
          │
          └──────────────► Financial Settlement
```

Both effects occur immediately when the Customer Return is created.

## Financial Settlement

```text
Customer Return Amount
          │
          ▼
Customer Total Outstanding Debt
          │
     ┌────┴────┐
     │         │
Debt >= Return  Debt < Return
     │         │
     ▼         ▼
Debt reduced   Debt → 0
by return      + Cash Refund
```

Cash is the supported refund method in the current phase.

No Accounting Journal Entry is generated for the Customer Return in the current scope.

## Deferred / Open Domain Details

The following remain outside the current Customer Return Domain Map decision:

- Exact configuration ownership for Return Splitting Policy.
- Detailed Return Settings model.
- Any future correction flow using a separate Sales transaction.

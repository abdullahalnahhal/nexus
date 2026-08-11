# NEXUS — Supplier Return Domain Addendum

> Phase 0.2 Inventory Discovery.
> Append-only domain documentation. Existing Domain Map history remains unchanged.

## Supplier Return

Supplier Return is an independent inventory/return document.

It does not require a Purchase Invoice. A Purchase Invoice, when available, is optional reference data.

### Required Data

```text
Supplier Return
├── Supplier
├── Representative
├── Return Warehouse
├── Items
│   └── Quantity per Item
├── Total Invoice Amount
└── Attachments
```

### Optional Data

```text
Supplier Return
├── Purchase Invoice Reference
└── Item-level Return Price
```

### Authorization Boundary

```text
User
  |
  +--> Permission to operate on Warehouse
           |
           v
    Supplier Return Operation
```

The domain does not define a hardcoded `Warehouse Manager` role as the authorization requirement.

### Inventory Effect

```text
Supplier Return Issued
        |
        v
Selected Warehouse
        |
        v
Stock deducted immediately
```

The aggregate quantity for a repeated Product must be available in the selected Warehouse.

### Financial Settlement Boundary

```text
Supplier Return
        |
        +--> Immediate Settlement
        |
        +--> Deferred Settlement
                    |
                    v
             Supplier actually settles
```

The settlement method is not fixed by the Supplier Return domain. The actual agreed method and amount are recorded, together with supporting settlement files.

### Relationship to Purchase Invoice

```text
Purchase Invoice (optional)
            |
            v
Supplier Return
```

The relationship is informational/reference data. The Supplier Return remains valid without a Purchase Invoice.

### Important Domain Distinction

Supplier Return is not modeled as the inverse implementation of Customer Return.

In particular:

- Customer Return requires an original Sales Invoice.
- Supplier Return does not require an original Purchase Invoice.
- Customer Return currently settles immediately and completely using Cash.
- Supplier Return supports immediate or deferred settlement and supplier-agreed settlement methods.

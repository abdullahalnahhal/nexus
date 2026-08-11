# NEXUS — Stock Adjustment Discovery

> Phase 0.2 Inventory Discovery — Stock Adjustment.
> Append-only discovery record. Previously established inventory rules remain unchanged and are not repeated as new decisions here.

## Status

**Stock Adjustment discovery decisions captured through the current Inventory Discovery checkpoint.**

## 1. Purpose

Stock Adjustment is used only for an allowed business reason or operation that requires an inventory quantity adjustment.

It is not a generic mechanism for arbitrarily increasing or decreasing stock.

## 2. Manual Creation

An authorized user may create a Stock Adjustment manually when the reason is one of the previously established allowed reasons/operations.

The user's permission is sufficient to issue the adjustment directly; no additional approval is required in the current phase.

## 3. Traceability

The reason and/or originating reference that caused the adjustment must be recorded inside the Stock Adjustment as traceability data.

The adjustment must therefore be traceable back to the business reason or originating operation that justified the inventory change.

## 4. Immediate Inventory Effect

A Stock Adjustment affects inventory **immediately when it is issued**.

```text
Issue Stock Adjustment
        |
        v
Inventory updated immediately
```

## 5. Repeated Products

A Stock Adjustment may contain the same Product more than once.

For the inventory effect, repeated lines for the same Product are considered together so that the resulting adjustment reflects their aggregate quantity.

## 6. Attachments

Attachments are not required for Stock Adjustment issuance in the current phase.

The Reason/Reference is sufficient for traceability.

## 7. Post-Issue Immutability

A Stock Adjustment cannot be modified after it is issued.

A Stock Adjustment cannot be cancelled after it is issued.

## 8. Accounting

Stock Adjustment has **no Accounting effect** in the current phase.

It does not create a General Ledger or Sub-ledger transaction.

Accounting and cost treatment for Stock Adjustment are outside the current scope.

## 9. Reference Number

Stock Adjustment does not require a separate independent Reference Number in the current phase.

## 10. Existing Shared Inventory Rules

The following rules were established previously and are intentionally not re-discovered here:

- Warehouse context and access are governed by the existing inventory/permission rules.
- The relevant previously established business operations/reasons that may cause inventory changes remain the authoritative source for allowed adjustment causes.
- UOM rules are deferred and are not part of the current Stock Adjustment discovery.

## 11. Current Discovered Flow

```text
Allowed Business Reason / Operation
             |
             v
     Authorized User
             |
             v
   Create Stock Adjustment
             |
             +--> Reason / Reference recorded
             |
             +--> Product(s) + Quantity(ies)
             |
             v
       Issue Adjustment
             |
             +--> Inventory updated immediately
             |
             +--> No Accounting effect
             |
             +--> Document becomes immutable
```

## 12. Explicitly Decided Constraints

The Stock Adjustment:

- Must be justified by an allowed reason or business operation.
- May be created manually by an authorized user when that reason/operation permits it.
- Must record the reason and/or originating reference for traceability.
- Takes effect on inventory immediately upon issuance.
- May contain the same Product more than once.
- Does not require Attachments for issuance.
- Does not require an additional Approval beyond the applicable Permission.
- Cannot be modified after issuance.
- Cannot be cancelled after issuance.
- Has no Accounting effect in the current phase.
- Does not require a separate independent Reference Number.
- Defers UOM considerations.

## 13. Still Open

No additional Stock Adjustment rule is being invented at this checkpoint. Any future unresolved detail will be recorded only when it becomes necessary and is explicitly discovered.

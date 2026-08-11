# NEXUS — Stock Adjustment Discovery

## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

> Append-only discovery record. Existing Inventory decisions are inherited and are not re-opened here.

## Purpose

Stock Adjustment represents a controlled inventory quantity change that must be justified by an allowed business reason and/or originating reference.

## Confirmed Decisions

1. A Stock Adjustment is not an unrestricted positive/negative stock edit.
2. The reason and/or originating reference must be recorded for traceability.
3. A user may create an Adjustment manually when the reason is allowed and the required Permission is granted.
4. The relevant Warehouse is governed by the existing Warehouse-access and Permission rules.
5. The inventory effect occurs immediately when the Adjustment is issued.
6. The same Product may appear on multiple lines in one Adjustment.
7. Repeated Product lines are aggregated when applying the inventory effect.
8. UOM is deferred from the current discovery scope.
9. Attachments are not required; Reason/Reference provides the required traceability.
10. No additional approval is required; the required Permission is sufficient for issuance.
11. An issued Stock Adjustment cannot be edited.
12. An issued Stock Adjustment cannot be cancelled.
13. Stock Adjustment has no accounting effect.
14. No separate Reference Number requirement is introduced in this phase.

## Lifecycle

```text
Authorized User
      ↓
Create Stock Adjustment
      ↓
Allowed Reason / Originating Reference
      ↓
Issue
      ↓
Immediate Stock Effect
      ↓
Immutable Historical Record
```

## Scope Boundary

The following are deliberately deferred:

- UOM rules.
- Cost accounting / valuation.
- Detailed configuration of the allowed-reason catalog.
- Any accounting integration.

## Related Documentation

- `stock-adjustment-business-rules-addendum.md`
- `stock-adjustment-domain-addendum.md`
- `stock-adjustment-glossary-addendum.md`
- `../learning/stock-adjustment-learning.md`
- `../references/stock-adjustment-references.md`
- `../planning/stock-adjustment-discovery-addendum.md`
- `../planning/stock-adjustment-vision-addendum.md`

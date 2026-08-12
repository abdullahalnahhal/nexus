# NEXUS — Stock Adjustment Learning

## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

### What we learned

1. A Stock Adjustment is an inventory business document, not a generic direct edit to stock.
2. Every adjustment must have an allowed reason and/or originating reference for traceability.
3. Manual creation is valid when the user has the required Permission and the selected reason is allowed.
4. The inventory effect occurs immediately when the Adjustment is issued.
5. The same Product may appear on multiple lines; the resulting inventory effect uses the aggregate quantity.
6. UOM behavior is deliberately deferred from this phase.
7. Reason/Reference is sufficient for traceability; Attachments are not required by this document.
8. Permission is sufficient for issuance; no additional approval workflow is introduced for this document.
9. Once issued, a Stock Adjustment is immutable: it cannot be edited or cancelled.
10. Stock Adjustment has no accounting effect in the current NEXUS scope.
11. A separate document reference-number requirement is not introduced in this phase.

### Domain insight

Stock Adjustment preserves the distinction between **business authorization** and **inventory state mutation**: authorization comes from Permissions, while issuance is the point at which the inventory state changes.

### Deferred topics

- UOM rules.
- Costing / inventory valuation.
- Any future accounting treatment.
- Detailed catalog design for allowed adjustment reasons.

---

## Documentation Synchronization — 2026-08-12

The finalized discovery also establishes that Stock Adjustment is a **permission-controlled inventory operation without an additional approval state**. This supersedes the earlier provisional wording that specifically referred to Warehouse Manager approval.

The final boundary is:

```text
Allowed Reason
      +
Required Permission
      ↓
Issue Stock Adjustment
      ↓
Immediate Stock Effect
```

The document itself is immutable after issuance, so later correction is not performed by editing or cancelling the issued Adjustment.
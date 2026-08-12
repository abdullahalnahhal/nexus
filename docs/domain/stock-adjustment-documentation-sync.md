# NEXUS — Stock Adjustment Documentation Sync

## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

This document records the synchronization of the completed Stock Adjustment discovery across the NEXUS documentation set. It is append-only and does not replace earlier discovery records.

## Finalized Business Decisions

- Stock Adjustment is not a generic arbitrary increase/decrease operation; every adjustment must be justified by an allowed reason and/or originating business reference.
- A user may create a Stock Adjustment manually when the relevant Permission is granted and the reason is allowed.
- Warehouse context and operational authorization follow the previously established Inventory access rules; they are not redefined here.
- A Stock Adjustment affects Current Stock immediately when issued.
- The same Product may appear on multiple lines in one Stock Adjustment. The resulting inventory effect uses the aggregate quantity for that Product.
- UOM is explicitly deferred from the current discovery scope.
- Attachments are not required for Stock Adjustment traceability; Reason/Reference is sufficient in the current scope.
- No additional Approval step is required. The required Permission is sufficient for direct issuance.
- Once issued, a Stock Adjustment cannot be edited.
- Once issued, a Stock Adjustment cannot be cancelled.
- Stock Adjustment has no accounting effect in the current scope.
- No separate Stock Adjustment reference-number requirement is introduced in the current scope.

## Documentation Consistency

The dedicated Stock Adjustment discovery, business-rules, domain, glossary, learning, planning, and reference addenda remain the detailed records. This synchronization document provides the consolidated checkpoint and prevents the same decisions from being rediscovered.

## Historical Rule Clarification

Earlier provisional documentation described Manual Edit/Quantity Adjustment as approval-controlled. The finalized Phase 0.2 discovery supersedes that assumption for Stock Adjustment specifically: Permission is sufficient and the document takes effect immediately on issuance.

This clarification does not change Approval rules for Transfer, Loss, Write-off/Depreciation, Opening Balance, or any other Inventory operation.

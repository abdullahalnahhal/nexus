# NEXUS — Phase 1 Document Foundation

## Status

**Phase:** 1 — Domain & System Foundations  
**Foundation:** Document Foundation  
**State:** Closed

## Purpose

This foundation establishes the shared document concepts used across NEXUS without forcing every Document type into one lifecycle or one business model.

## Decisions

- Every Document has a technical Unique Identifier.
- Every Document has a shared `status` field; allowed values and transitions are Document-specific.
- Each Document has its own lifecycle according to business nature.
- Editability after issuance is governed by the Document's own business rules.
- Line deletion is governed by the parent Document's business rules.
- Every Document Line has an independent Technical Unique Identifier.
- Every Document Line directly references the Product/Item involved.
- Line order is a UI concern and has no business meaning.
- A Document that depends on another Document stores a direct reference to the originating Document.
- Document References explicitly record the relationship type.
- A Document normally has at most one Document Reference; multiple references are allowed only when the Document nature requires them.
- A Document Reference is created before issuance, is immutable after creation, cannot be deleted, and its creation is recorded in history/activity.
- An operationally scoped Document directly references the applicable Branch, Warehouse, and/or POS.
- Company is implicit because the current NEXUS model is single-company.
- Every issuable Document stores `issued_by` and `issued_at`.
- Every cancellable Document stores `cancelled_by`, `cancelled_at`, `cancel_reason`, and `cancel_notes` when cancelled.
- Cancellation representation is Document/process-specific.
- Cancellation reasons are predefined according to the applicable Document rules, with optional notes.
- Every Document stores creation metadata: `created_by` and `created_at`.
- Shared entity/document metadata includes `created_at`, `updated_at`, `deleted_at`, `created_by`, `is_removable`, `is_hidden`, `is_editable`, and `status`.
- `is_removable`, `is_hidden`, and `is_editable` are explicit persisted values; their behavior is Document/Entity-specific.
- User activity is tracked through Spatie Activity Log.
- Business History is separate from user activity and is defined per Document/Domain when required.
- Attachments use Spatie Media Library and are limited to image/PDF files. Attachment cardinality and mandatory/optional/conditional requirements are Document/process-specific.
- Notes/Comments are Document-specific.
- Company currency is inherited by Documents; Documents do not need an independent currency selection in the current model.
- Financial Documents may persist `Subtotal`, `Discounts`, `Additions`, `Total`, `Paid Amount`, `Remaining Amount`, and `Overpaid Amount` when applicable.
- `Discounts` and `Additions` are currently stored as aggregate values, one of each per Document.
- `Total` is persisted and recalculated automatically when editable Line data changes.
- Financial field relationships are Document-specific. In particular, no universal relationship is imposed between `Total`, `Paid Amount`, `Remaining Amount`, and `Overpaid Amount`.
- Financial Documents may contain multiple Payment Entries.
- Each Payment Entry has an independent technical Unique Identifier and stores at least `payment_method` and `amount`.
- Payment Entry edit/delete behavior follows the parent Document lifecycle.
- Payment Entry activity is covered by the parent Document's Activity/Business History; it does not require a separate universal audit model.
- Product master data is referenced directly rather than duplicated as a generic snapshot; logical deletion preserves the referenced Product record and its history.

## Explicitly Not Unified

The following remain intentionally Document-specific:

- Lifecycle states and transitions.
- Whether issuance exists.
- Whether cancellation exists and how it is represented.
- Line edit/delete rules.
- Business reasons and reason catalogs.
- Business History structure.
- Attachment requirements.
- Notes/Comments.
- Financial-field relationships.
- Payment-specific rules.

## Foundation Boundary

This document defines the common vocabulary and invariants only. It does not replace the detailed Business Rules or Domain Discovery records for Sales, Purchases, Returns, Inventory, Orders, or Payments.

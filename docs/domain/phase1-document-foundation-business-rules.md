# NEXUS — Phase 1 Document Foundation Business Rules

## Checkpoint

Phase 1 — Document Foundation

## Rules

### BR-DOC-FND-001 — Technical Document Identity
Every Document has a unique technical identifier.

### BR-DOC-FND-002 — Shared Status
Every Document has a `status` field. Allowed statuses and transitions are defined by the Document lifecycle.

### BR-DOC-FND-003 — Document-Specific Lifecycle
Each Document type defines its own lifecycle according to business nature.

### BR-DOC-FND-004 — Document-Specific Editability
Whether an Issued Document may be edited is governed by its own business rules.

### BR-DOC-FND-005 — Document Line Identity
Every Document Line has an independent technical identifier.

### BR-DOC-FND-006 — Product Reference
Every Document Line directly references the Product/Item it represents.

### BR-DOC-FND-007 — Line Order
Document Line order has no business significance and may change without business effect.

### BR-DOC-FND-008 — Document Reference
A dependent Document stores a direct reference to its originating Document and the relationship type.

### BR-DOC-FND-009 — Reference Cardinality
A Document has at most one Document Reference by default. Multiple references are allowed only when the Document's nature requires them.

### BR-DOC-FND-010 — Reference Immutability
A Document Reference is immutable and cannot be deleted after creation.

### BR-DOC-FND-011 — Reference Timing
A required Document Reference must be created before issuance.

### BR-DOC-FND-012 — Reference Activity
Creation of a Document Reference is recorded through the applicable activity/history mechanism.

### BR-DOC-FND-013 — Operational Scope
A Document stores direct references to its Branch, Warehouse, and/or POS when the business operation is associated with those scopes.

### BR-DOC-FND-014 — Issuance Metadata
An issuable Document stores `issued_by` and `issued_at`.

### BR-DOC-FND-015 — Cancellation Metadata
A cancellable Document stores `cancelled_by`, `cancelled_at`, `cancel_reason`, and `cancel_notes` when cancelled.

### BR-DOC-FND-016 — Cancellation Reasons
Cancellation reasons are selected from an allowed list defined for the Document/process, with optional notes.

### BR-DOC-FND-017 — Shared Metadata
The common persisted metadata is:

`created_at`, `updated_at`, `deleted_at`, `created_by`, `is_removable`, `is_hidden`, `is_editable`, and `status`.

### BR-DOC-FND-018 — Metadata Behavior
`is_removable`, `is_hidden`, and `is_editable` are explicit persisted values. Their change rules are Entity/Document-specific.

### BR-DOC-FND-019 — Activity Logging
User activity is captured through Spatie Activity Log.

### BR-DOC-FND-020 — Business History
Business History is Document/Domain-specific and is not forced into one universal history model.

### BR-DOC-FND-021 — Attachments
Attachments use Spatie Media Library and are limited to images and PDF files. Mandatory/optional/conditional requirements are Document/process-specific.

### BR-DOC-FND-022 — Company Context
The current single Company is implicit; Documents do not require a `company_id`.

### BR-DOC-FND-023 — Company Currency
Currency is defined at Company level and is inherited by applicable Documents.

### BR-DOC-FND-024 — Financial Totals
Applicable Documents may persist `Subtotal`, `Discounts`, `Additions`, and `Total`.

### BR-DOC-FND-025 — Persisted Total
`Total` is stored on the Document and automatically recalculated when editable Line data changes.

### BR-DOC-FND-026 — Financial Payment Values
Applicable Documents may persist `Paid Amount`, `Remaining Amount`, and `Overpaid Amount`.

### BR-DOC-FND-027 — Financial Relationships
Relationships among financial amount fields are defined by each Document's business rules; no universal formula is imposed.

### BR-DOC-FND-028 — Payment Entries
A Financial Document may contain multiple Payment Entries. Each Entry has a unique technical identifier, `payment_method`, and `amount`.

### BR-DOC-FND-029 — Payment Entry Lifecycle
Payment Entry edit/delete behavior follows the parent Document lifecycle.

### BR-DOC-FND-030 — Product Historical Reference
Document Lines retain the Product reference rather than duplicating Product master data as a generic snapshot. Logical deletion preserves historical Product records.

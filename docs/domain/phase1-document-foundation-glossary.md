# NEXUS — Phase 1 Document Foundation Glossary

## Document
A business record representing an operation in NEXUS. Its lifecycle and rules are determined by its business nature.

## Document Line
An independent line within a Document with its own technical identifier and a direct Product/Item reference.

## Document Reference
A relationship from one Document to another Document, including the referenced Document and the relationship type.

## Payment Entry
A payment component inside a Financial Document. It has its own technical identifier, Payment Method, and Amount.

## Document Status
The persisted current lifecycle state of a Document. Allowed values and transitions are Document-specific.

## Issuance
The lifecycle operation through which an issuable Document becomes issued. Issuable Documents store Issued By and Issued At.

## Cancellation
A Document-specific lifecycle/process action that may be represented as status/metadata or as a separate business record according to the business nature.

## Shared Metadata
Common persisted fields used by NEXUS entities/documents: created_at, updated_at, deleted_at, created_by, is_removable, is_hidden, is_editable, and status.

## User Activity Log
The technical/user activity trail captured through Spatie Activity Log.

## Business History
Domain-specific historical information required by a business process. It is not the same concept as User Activity Logging.

## Subtotal
The persisted Document amount before Discounts and Additions.

## Discounts
The aggregate persisted discount value on a Document, when applicable.

## Additions
The aggregate persisted additional-charge value on a Document, when applicable.

## Total
The persisted calculated Document total, recalculated when editable Line data changes.

## Paid Amount
The amount paid against a Financial Document when applicable.

## Remaining Amount
The outstanding amount for a Financial Document when applicable.

## Overpaid Amount
The amount by which Paid Amount may exceed Total when the specific Document rules permit overpayment.

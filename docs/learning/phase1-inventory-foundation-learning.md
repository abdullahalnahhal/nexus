# NEXUS — What We Learned

## Phase 1 — Inventory Foundation / Domain Boundaries

### Learning 1 — State and Event Are Different Concepts

We separated:

- `Current Stock` as current state;
- `Stock Movement` as the historical inventory effect;
- `Inventory Document` as the business transaction.

This prevents the inventory model from collapsing business meaning, historical effects, and current state into one entity.

### Learning 2 — A Business Document Does Not Necessarily Equal One Inventory Movement

A Transfer is the clearest example. One Transfer Document produces two movements: OUT from the source warehouse and IN to the destination warehouse.

Therefore the relationship is:

`Document 1 → Movement 1..N`

### Learning 3 — Current Stock Is Not a Ledger

Current Stock answers: “What is the quantity now?”

Stock Movement answers: “What inventory effect occurred?”

The two concepts should not be conflated.

### Learning 4 — Immutable Inventory Effects Improve Auditability

Once a Stock Movement exists, changing it would rewrite inventory history. Therefore corrections are represented by new business documents and new movements.

### Learning 5 — Inventory Quantity and Financial Cost Are Separate Concerns

The current domain decision is:

- Stock Movement → Quantity
- Invoice/Inventory Document → Quantity + Cost where applicable

This avoids introducing accounting valuation concerns into the inventory movement boundary prematurely.

### Learning 6 — Atomicity Matters at the Inventory Boundary

A Transfer cannot partially update inventory. The source OUT and destination IN must succeed together.

### Learning 7 — Authorization Is a Permission Concern

Inventory approval and adjustment availability are determined by permissions, not by a hardcoded `Manager` role.

## What These Learnings Influence

These decisions guide aggregate boundaries, transaction boundaries, persistence design, audit design, approval workflows, correction/reversal strategies, and future accounting integration.

They do not reopen previously settled business rules.

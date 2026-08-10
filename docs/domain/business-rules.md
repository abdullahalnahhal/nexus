# NEXUS — Business Rules

> Business rules are identified during Domain Discovery.
> IDs are provisional until the Domain Map is finalized.

## Branch & Warehouse

### BR-001 — POS Branch Ownership

A POS belongs to exactly one Branch.

### BR-002 — POS Non-Transferability

A POS cannot be transferred from one Branch to another.

### BR-003 — Warehouse Branch Ownership

A Warehouse belongs to exactly one Branch.

### BR-004 — Warehouse Non-Transferability

A Warehouse cannot be transferred from one Branch to another.

---

## Users & Access

### BR-005 — Multi-Branch User

A User may operate across multiple Branches.

### BR-006 — POS Assignment

A User may operate only on POSes to which the User is assigned.

### BR-007 — Sales Eligibility

A POS assignment may specify whether the assigned User is allowed to perform sales operations.

### BR-008 — Authentication Before Access

A User must authenticate into NEXUS before accessing protected functionality.

---

## POS

### BR-009 — POS Operations

A physical POS performs Sales and Returns.

### BR-010 — POS Purchase Restriction

A physical POS does not perform Purchase operations.

### BR-011 — POS Wallet

Each POS has its own Wallet.

### BR-012 — Branch Warehouse Context

A POS operates against the Warehouse belonging to its Branch.

---

## Shift

### BR-013 — Shift Salesman

A Shift has one Salesman.

### BR-014 — Shift Managers

A Shift may have multiple Managers.

### BR-015 — Salesman Shift Exclusivity

A Salesman cannot operate on two POSes simultaneously within the same Shift context.

### BR-016 — Manager Multi-POS Participation

A Manager may participate in multiple POSes within the same Shift.

### BR-017 — Shift Continuity

A new Shift cannot start for a POS until the previous Shift has completed the required closing and confirmation process.

---

## Shift Closing

### BR-018 — Branch Settlement Confirmation

A POS-to-Branch settlement requires confirmation from a Branch Manager.

### BR-019 — Settlement Financial Effect

After confirmed settlement:

```text
POS Wallet   -X
Branch Wallet +X
```

### BR-020 — REMAIN

A Shift may end through REMAIN instead of transferring the POS balance to the Branch Wallet.

### BR-021 — REMAIN Confirmation

REMAIN requires confirmation by either the incoming Manager or incoming Salesman.

### BR-022 — REMAIN Continuity

After REMAIN confirmation, the carried amount continues into the next Shift's POS financial context.

---

## Customers

### BR-023 — Customer Grades

An existing customer has one of the following grades:

* Blocked
* Normal
* Premium
* VIP

### BR-024 — Blocked Customer

A Blocked customer cannot make a Sale until the block is removed.

### BR-025 — Takeaway Full Payment

A Takeaway Sale must be fully paid at the time of Sale.

### BR-026 — Identified Customer Remaining

An identified customer may have a Remaining amount on a Sale.

### BR-027 — Customer Receivable

A Remaining amount is recorded as a receivable/debt against the customer for the Branch.

### BR-028 — Receivable Is Not Cash

A customer receivable does not increase the Branch's physical cash balance.

---

## Payment

### BR-029 — Supported Payment Methods

Physical NEXUS currently supports:

* Cash
* Visa

### BR-030 — POS Wallet Payment Effect

The amount actually received from the customer increases the POS Wallet.

---

## Inventory

### BR-031 — Sale Inventory Effect

A completed Sale decreases the relevant Branch Warehouse stock.

### BR-032 — Return Inventory Effect

A completed Return may increase the relevant Branch Warehouse stock.

> Inventory validation and exact transaction timing remain under discovery.

---

## Deferred Domain

### BR-033 — Online Customer Scope

Online Customer operations are outside the current physical NEXUS scope.

### BR-034 — Online Warehouse Scope

The Online Customer Warehouse is deferred until the physical NEXUS domain is completed.

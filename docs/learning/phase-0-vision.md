# NEXUS — Learning Notes

# Phase 0 — Vision & Business Discovery

## 1. What This Phase Was Really About

The purpose of Phase 0 was not to design the database or start coding.

The purpose was to learn how to understand a business system before designing its technical solution.

The working sequence became:

```text
Business Understanding
        ↓
Business Concepts
        ↓
Business Rules
        ↓
Domain Model
        ↓
Architecture
        ↓
Implementation
```

---

## 2. Business First

A major lesson was the difference between:

> "What tables do we need?"

and:

> "What business concepts actually exist?"

For example, POS is not merely a database table.

It represents an operational business point with:

* Wallet
* Shifts
* Sales
* Returns
* User assignments
* Business restrictions

---

## 3. Ownership vs Association

A major discovery was that not every relationship means ownership.

Examples:

```text
Branch → POS
Branch → Warehouse
```

represent strong structural relationships.

But:

```text
User ↔ Branch
User ↔ POS
```

represent operational access/assignment relationships.

A User can work across multiple Branches and POSes without belonging exclusively to one.

---

## 4. Role vs Permission vs Assignment

Another important lesson:

These are different concepts.

### Role

Describes the user's business responsibility.

### Permission

Describes what actions the user is allowed to perform.

### POS Assignment

Describes which POSes the user may operate and potentially whether the user can sell on them.

Therefore:

```text
User
 ├── Role
 ├── Permissions
 └── POS Assignments
```

should not automatically be collapsed into one concept.

---

## 5. Shift as a Business Concept

The Shift initially looked like a time period.

Domain discovery showed that it is much more important.

A Shift represents an operational and financial accountability period for a POS.

It controls:

* Assigned personnel
* POS operation
* Financial closing
* Settlement
* REMAIN
* Confirmation before the next Shift

This is an example of discovering a domain concept through business behavior rather than through data fields.

---

## 6. Financial Effects Are Not Just Balances

A key lesson from the Sale flow:

A Sale may produce different financial effects.

Example:

```text
Sale Total = 1,000
Paid = 700
Remaining = 300
```

The system should conceptually represent:

```text
POS receives 700
Customer owes 300
Branch has a receivable of 300
```

The 300 is not physical cash.

Therefore:

> A financial balance and a financial claim are not necessarily the same thing.

---

## 7. Business Rules Should Be Explicit

Rules discovered during conversation should not disappear inside implementation details.

They are documented separately and receive stable IDs.

Example:

```text
BR-024 — Blocked Customer

A Blocked customer cannot make a Sale
until the block is removed.
```

Later, these rules can be traced to:

```text
Business Rule
    ↓
Domain/Application Logic
    ↓
Automated Test
```

---

## 8. Domain Map vs Business Rules vs Glossary

Three documentation artifacts have different responsibilities.

### Domain Map

Answers:

> What concepts exist and how are they related?

### Business Rules

Answers:

> What must or must not happen?

### Glossary

Answers:

> What does each business term mean specifically in NEXUS?

This separation keeps the documentation focused.

---

## 9. Important Discovery Method

A useful technique discovered during Phase 0 is to ask:

* What is this concept?
* Why does it exist?
* What can it do?
* What can it not do?
* What does it interact with?
* What happens before it?
* What happens after it?
* What rules constrain it?
* Who is responsible for it?

The answers gradually reveal the Domain Model.

---

## 10. Current Staff-Level Learning Goal

The purpose of NEXUS is not only to build a working application.

It is also a practical exercise in Staff-level engineering thinking:

* Understanding business domains
* Identifying boundaries
* Modeling business behavior
* Making rules explicit
* Separating ownership from association
* Identifying invariants
* Designing around business capabilities
* Connecting business rules to implementation and tests

The target is to move from:

> "I know how to implement the feature."

toward:

> "I understand the business problem, can model it, identify its constraints, and design a sustainable solution."

---

## 11. Current Discovery State

Phase 0 Vision is considered complete.

Phase 0.2 Domain Discovery is in progress.

Current discovered concepts include:

* Branch
* Warehouse
* POS
* User
* Role
* Permission
* POS Assignment
* Shift
* Manager
* Salesman
* Sale
* Return
* Customer
* Customer Grade
* POS Wallet
* Branch Wallet
* Customer Receivable

Online Customer and Online Warehouse are intentionally deferred.

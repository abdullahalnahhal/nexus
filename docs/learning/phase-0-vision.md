# Phase 0 — Vision

## What I Learned

---

## 1. From Feature Thinking to Business Thinking

Before NEXUS, my natural approach could be:

```text
Feature
   ↓
Code
   ↓
Database
```

During NEXUS, I learned to start from:

```text
Business Problem
       ↓
Business Reality
       ↓
Business Concepts
       ↓
Business Rules
       ↓
Business Flows
       ↓
Domain Model
       ↓
Architecture
       ↓
Code
```

### What I Learned

A software system should not start from tables, models, or APIs.

It should start by understanding the business that the software is supposed to represent.

---

## 2. Understanding the System Boundary

NEXUS represents one company operating through multiple branches.

We deliberately decided not to introduce:

* `Company` entity
* `Tenant` entity
* Multi-tenancy

### What I Learned

Not every real-world concept needs to become a software entity.

An abstraction should exist because the system needs it, not because it sounds architecturally complete.

This taught me to ask:

> Does this concept have independent business meaning and behavior?

before creating an entity for it.

---

## 3. Modeling the Real Business

Instead of starting with database relationships, we started by asking:

> How does the business actually operate?

This led to:

```text
NEXUS
│
├── Branches
│
├── Warehouses
│
└── Wallets
```

A Branch represents a physical business location.

A Branch has:

```text
Branch
├── Warehouse
├── POS[]
└── Wallet
```

### What I Learned

Domain modeling means discovering the concepts and relationships that exist in the real business.

It is not simply designing database tables.

---

## 4. Entity vs Business Concept

We initially discussed POS and Cash Register separately.

After analyzing the real business meaning, we decided:

```text
POS = Cash Register
```

Therefore, there is no separate `CashRegister` entity.

### What I Learned

Not every noun in a business vocabulary deserves its own entity.

Two different names may represent the same business concept.

Before creating an entity, I should ask:

* Does it have independent identity?
* Does it have independent lifecycle?
* Does it have independent behavior?
* Is it actually different from an existing concept?

---

## 5. Relationships Have Business Meaning

We did not define:

```text
POS
└── warehouse_id
```

Instead, we discovered:

```text
POS
 ↓
Branch
 ↓
Warehouse
```

Every POS uses the Warehouse of its Branch.

### What I Learned

A relationship is not just a foreign key.

It represents a business rule.

The important question is not:

> How do I store this relationship?

but:

> Why does this relationship exist?

---

## 6. Avoiding Premature Abstraction

We deliberately avoided introducing concepts that are not currently required.

Examples:

* Company
* Tenant
* POS-specific Warehouse
* Separate CashRegister entity

### What I Learned

Good architecture is not about having the largest number of abstractions.

Good architecture means having the abstractions that correctly represent the current business.

> **Abstract when the business gives you a reason to abstract.**

---

## 7. Transaction Thinking

Inventory changes are not treated as simple field updates.

Instead:

```text
Warehouse
   ↓
Inventory Transaction
   ↓
Stock Change
```

Financial changes follow the same principle:

```text
Wallet
   ↓
Financial Transaction
   ↓
Balance Change
```

Warehouse transactions include:

```text
IN
OUT
TRANSFER
```

Wallet transactions include:

```text
INCOME
OUTCOME
TRANSFER
```

### What I Learned

Important business changes should be represented as business transactions rather than unexplained state mutations.

This provides:

* Traceability
* Auditability
* History
* Debuggability
* Business accountability

---

## 8. Unified Financial Modeling

Instead of creating separate financial logic for:

```text
Bank Account
Branch Account
POS Account
Cash Account
```

we introduced:

```text
Wallet
   ↓
Wallet Transaction
```

Different financial contexts can use the same financial abstraction.

Examples:

```text
Bank Wallet
Branch Wallet
POS Wallet
```

### What I Learned

When multiple concepts share the same real business behavior, a common domain abstraction can reduce duplication and keep the model consistent.

But the abstraction must come from genuine shared behavior, not from a desire to make the design "generic".

---

## 9. Business Process Thinking

The Order is not an isolated CRUD record.

The real sales process is:

```text
Salesman
   ↓
POS
   ↓
Shift
   ↓
Order
   ├── Inventory OUT
   └── Financial INCOME
```

The Order exists inside a larger business process.

### What I Learned

A feature should be understood as part of a business workflow rather than as an isolated database operation.

Instead of asking:

> What fields does Order have?

I should also ask:

> What business process creates the Order?

> Who is allowed to create it?

> What state must the business be in?

> What other business effects happen because of it?

---

## 10. Business Rules Before Code

During the Vision phase, we started identifying explicit rules.

Examples:

```text
Every Branch has exactly one Warehouse.

Every Branch has one Wallet.

Every Branch can have many POS terminals.

Every POS belongs to exactly one Branch.

A POS uses its Branch Warehouse.

A POS can have only one active Shift.

Each Shift belongs to exactly one Sales Employee.
```

### What I Learned

Business rules should be explicit before implementation.

If a rule exists only inside someone's head or inside controller code, it is difficult to protect and maintain.

---

## 11. State and Lifecycle Thinking

The Shift introduced the idea that business entities have lifecycles.

For example:

```text
Shift
  ↓
OPEN
  ↓
ACTIVE
  ↓
CLOSED
```

And:

```text
POS
  ↓
No Active Shift
  ↓
Open Shift
  ↓
Active Shift
  ↓
Close Shift
```

### What I Learned

Business entities are not always just data.

Many of them have:

* States
* Transitions
* Preconditions
* Actions
* Lifecycle rules

This is an important part of domain modeling.

---

## 12. Understanding Ownership

We started distinguishing between:

* Ownership
* Association
* Usage

For example:

```text
Branch
 └── Warehouse
```

while:

```text
POS
 ──uses──> Branch Warehouse
```

The POS does not own the Warehouse.

Similarly, a User is not owned by a POS merely because that User is authorized to operate it.

### What I Learned

Not every relationship means ownership.

I should distinguish between:

```text
owns
belongs to
uses
references
is authorized to use
```

because each relationship has different business meaning.

---

## 13. From CRUD Thinking to Domain Thinking

CRUD asks:

```text
Create
Read
Update
Delete
```

Domain thinking asks:

```text
What happened?

Who can make it happen?

Under what conditions?

What changes because of it?

What rules must remain true?

What transaction records the event?
```

### What I Learned

CRUD is an implementation mechanism.

The business domain is the thing being implemented.

---

## 14. The Most Important Lesson

The biggest lesson from Phase 0 is:

```text
Business Problem
       ↓
Business Reality
       ↓
Business Concepts
       ↓
Relationships
       ↓
Business Rules
       ↓
Business Flows
       ↓
Domain Model
       ↓
Architecture
       ↓
Implementation
```

I should not reverse this process by starting with:

```text
Database
   ↓
Models
   ↓
Controllers
   ↓
Business Logic
```

---

## 15. Staff-Level Skills Practiced

Through Phase 0, I practiced the following skills:

* Business analysis
* Domain modeling
* Identifying business boundaries
* Identifying entities and concepts
* Distinguishing entities from abstractions
* Modeling relationships
* Identifying business rules
* Modeling business workflows
* Thinking in transactions
* Thinking in lifecycles and states
* Avoiding premature abstraction
* Designing from business behavior rather than database structure

These are not only software implementation skills.

They are part of the transition from:

```text
Senior Software Developer
```

toward:

```text
Staff-level Engineer
```

---

## 16. Questions I Should Now Ask

After completing the Vision phase, I should be able to approach the next phase with questions such as:

### About the Domain

* What are the real business entities?
* What are their responsibilities?
* Who owns what?
* Who uses what?
* What are their lifecycles?

### About Rules

* What must always be true?
* What operations are allowed?
* What operations are forbidden?
* What conditions must exist before an operation?

### About Processes

* What triggers the process?
* Who performs it?
* What changes?
* What transactions are generated?
* What happens if something fails?

### About Architecture

* Where should each rule live?
* What should be an Aggregate?
* What should be an Entity?
* What should be a Value Object?
* What should be a Domain Service?
* What should be a Domain Event?

---

## 17. Phase 0 Completion Criteria

I consider the Vision phase successful when I can explain NEXUS without talking about:

* Tables
* Columns
* Controllers
* Frameworks
* APIs
* Laravel
* PHP

and instead explain it entirely through:

```text
Business Concepts
Business Relationships
Business Rules
Business Processes
Business Transactions
```

Only after that should implementation begin.

---

## 18. Personal Progress

### Before Phase 0

I was primarily thinking as a developer implementing requested features.

### After Phase 0

I am learning to think as an engineer who first understands the business problem, models the domain, identifies rules and workflows, and then chooses the technical implementation.

The goal is not simply to write better code.

The goal is to become better at **designing systems**.

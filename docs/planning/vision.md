# NEXUS — Vision

## 1. Vision

**NEXUS** is a business management system designed for a single company operating through multiple branches.

The system provides a unified model for managing:

* Branches
* Warehouses & Inventory
* Points of Sale (POS)
* Orders & Sales
* Users & Work Shifts
* Wallets & Financial Transactions

The core goal of NEXUS is to model the real operational flow of a retail/supply-chain business rather than treating the system as a collection of CRUD modules.

---

## 2. Business Structure

NEXUS represents **one company**.

There is no `Company` entity and no multi-tenancy concept in the initial version.

```text
NEXUS
│
├── Branches
│   ├── Branch A
│   ├── Branch B
│   └── ...
│
├── Warehouses
│   ├── Warehouse A
│   ├── Warehouse B
│   └── ...
│
└── Wallets
    ├── Bank Accounts
    ├── Branch Wallets
    ├── POS Wallets
    └── ...
```

---

## 3. Branches

A **Branch** represents a physical business location operated by NEXUS.

Each Branch has:

* One Warehouse
* Multiple POS terminals
* One Branch Wallet

```text
Branch
│
├── Warehouse
│
├── POS
│   ├── POS A
│   ├── POS B
│   └── ...
│
└── Wallet
```

### Branch Rules

1. Every Branch MUST have exactly one Warehouse.
2. Every Branch MUST have one Branch Wallet.
3. A Branch can have many POS terminals.

The Branch Warehouse is the inventory source used by all POS terminals belonging to that Branch.

---

## 4. Warehouses

A **Warehouse** represents a physical inventory location.

NEXUS can have multiple Warehouses.

Examples:

```text
NEXUS
│
├── Central Warehouse
├── Branch A Warehouse
├── Branch B Warehouse
└── ...
```

A Warehouse is responsible for holding stock and recording inventory movements.

### Warehouse Transactions

Warehouse stock changes through inventory transactions:

```text
Warehouse
│
└── Transactions
    ├── IN
    ├── OUT
    └── TRANSFER
```

### Receiving Stock

```text
Supplier
   │
   ▼
Warehouse
   │
   └── IN
```

### Transferring Stock

```text
Central Warehouse
        │
        │ TRANSFER
        ▼
Branch A Warehouse
```

### Selling Stock

```text
Branch A POS
      │
      ▼
    Order
      │
      ▼
Branch A Warehouse
      │
      └── OUT
```

The Order does not directly own inventory.

The resulting inventory movement is recorded as a Warehouse transaction.

---

## 5. POS — Point of Sale / Cash Register

A **POS is the Cash Register**.

They are the same business entity in NEXUS.

A POS represents the actual sales point where a salesman operates, orders are created, payments are received, and the active work shift is managed.

A POS:

* Belongs to exactly one Branch.
* Creates Orders.
* Uses the Warehouse of its Branch automatically.
* Has a Wallet.
* Has authorized Users.
* Operates through Work Shifts.

### POS and Warehouse

A POS does **not** have its own Warehouse.

The inventory relationship is:

```text
POS
 ↓
Branch
 ↓
Warehouse
```

Therefore, all POS terminals belonging to the same Branch operate against the same Branch Warehouse.

Example:

```text
Branch A
│
├── Warehouse A
│
├── POS A1 ─────┐
├── POS A2 ─────┼──> Warehouse A
└── POS A3 ─────┘
```

All sales made through POS A1, POS A2, and POS A3 affect the stock in Warehouse A.

### POS Wallet

Each POS has a Wallet.

```text
POS
│
├── Wallet
├── Users
└── Shifts
```

The POS Wallet records financial movements resulting from sales and other operations performed through the POS.

---

## 6. Orders

An Order is created from a POS.

The basic sales flow is:

```text
Customer
   │
   ▼
POS
   │
   ▼
Order
   │
   ├── Payment
   │
   └── Inventory Movement
          │
          ▼
      Branch Warehouse
```

Therefore, an Order is associated with the operational context in which it was created:

```text
Order
 └── POS
      └── Branch
           └── Warehouse
```

This allows NEXUS to determine automatically:

* Which Branch made the sale.
* Which POS created the Order.
* Which Warehouse supplies the products.
* Which financial Wallet receives the payment.
* Which Work Shift was active when the Order was created.

---

## 7. Wallets

NEXUS uses a unified **Wallet** concept for financial accounts.

Instead of creating separate transaction systems for every financial entity, all financial balances are represented through Wallets.

```text
Wallet
│
└── Transactions
    ├── INCOME
    ├── OUTCOME
    └── TRANSFER
```

NEXUS may contain different types of Wallets, including:

* Bank Account Wallet
* Branch Wallet
* POS Wallet
* Other financial wallets as required

### Wallet Transactions

Wallet balances change through financial transactions:

```text
Wallet A
   │
   ├── INCOME
   ├── OUTCOME
   └── TRANSFER
```

For example:

```text
POS Wallet
    │
    │ TRANSFER
    ▼
Branch Wallet
```

---

## 8. Branch Wallet

Each Branch has one Wallet representing its financial safe/account.

```text
Branch A
│
├── Warehouse A
├── POS A1
├── POS A2
└── Branch Wallet
```

The Branch Wallet represents the financial balance belonging to that Branch.

It can receive money from POS Wallets and participate in other financial operations.

---

## 9. Work Shifts

A **Work Shift** represents a period during which a Sales Employee is responsible for operating a POS.

```text
POS
│
└── Shifts
    ├── Shift #001 → Salesman A
    ├── Shift #002 → Salesman B
    └── ...
```

### Shift Rules

1. A POS can have many historical Shifts.
2. A POS can have only one active Shift at a time.
3. Each Shift is assigned to exactly one Sales Employee.
4. Orders created during a Shift belong to that Shift's operational context.

Example:

```text
POS A1
   │
   └── Active Shift #105
          │
          └── Salesman Abdullah
                 │
                 ├── Order #1001
                 ├── Order #1002
                 └── Order #1003
```

---

## 10. Users & Permissions

Users are not owned by a POS.

Instead, users have roles, permissions, and operational access.

```text
User
│
├── Roles
└── Permissions
```

Examples of permissions:

```text
VIEW_INVENTORY
CREATE_ORDER
OPEN_SHIFT
CLOSE_SHIFT
VIEW_SALES
...
```

A Sales Employee may be authorized to operate a specific POS during a Shift.

The ability to view inventory, create orders, open shifts, close shifts, or perform other operations is controlled through permissions.

---

## 11. Core Business Flow

The primary retail flow in NEXUS is:

```text
                    NEXUS
                      │
                    Branch
                      │
          ┌───────────┴───────────┐
          │                       │
      Warehouse                  POS
          │                       │
          │                 Active Shift
          │                       │
          │                     User
          │                       │
          │                     Order
          │                       │
          │              ┌────────┴────────┐
          │              │                 │
          ▼              ▼                 ▼
       Inventory      Payment          Customer
       Movement          │
          │              ▼
          │          POS Wallet
          │
          └──────────────┘
```

The POS is the operational point that connects:

* Sales
* Orders
* Customers
* Work Shifts
* Payments
* POS Wallet
* Branch
* Branch Warehouse

---

## 12. Fundamental Relationships

The current NEXUS model can be summarized as:

```text
NEXUS
│
├── Branches
│   │
│   └── Branch
│       ├── Warehouse (1)
│       ├── POS (N)
│       │   ├── Wallet (1)
│       │   ├── Users / Access
│       │   └── Shifts (N)
│       │       └── Salesman (1)
│       │
│       └── Wallet (1)
│
├── Warehouses
│   └── Warehouse Transactions
│
└── Wallets
    └── Wallet Transactions
```

### Key Relationships

```text
NEXUS
  ├── has many Branches
  ├── has many Warehouses
  └── has many Wallets

Branch
  ├── has one Warehouse
  ├── has many POS
  └── has one Wallet

POS
  ├── belongs to one Branch
  ├── uses its Branch Warehouse
  ├── has one Wallet
  ├── has many historical Shifts
  └── has one active Shift at most

Shift
  └── belongs to one Sales Employee

Warehouse
  └── has many Inventory Transactions

Wallet
  └── has many Financial Transactions

Order
  ├── belongs to one POS
  ├── belongs to one Shift
  └── operates against the POS's Branch Warehouse
```

---

## 13. Core Business Rules

### Branch

1. NEXUS has many Branches.
2. Every Branch has exactly one Warehouse.
3. Every Branch has one Branch Wallet.
4. A Branch can have many POS terminals.

### Warehouse

5. NEXUS can have many Warehouses.
6. A Warehouse records inventory transactions.
7. Inventory movements are represented by IN, OUT, and TRANSFER operations.

### POS

8. Every POS belongs to exactly one Branch.
9. POS and Cash Register are the same entity.
10. A POS does not own a Warehouse.
11. A POS automatically operates against its Branch Warehouse.
12. A POS has one Wallet.
13. A POS creates Orders.
14. A POS can have many historical Shifts.
15. A POS can have only one active Shift at a time.

### Wallet

16. NEXUS can have many Wallets.
17. Branches have Wallets.
18. POS terminals have Wallets.
19. Wallets record INCOME, OUTCOME, and TRANSFER transactions.

### Shift

20. Each Shift is assigned to exactly one Sales Employee.
21. A Sales Employee can operate a POS through an active Shift.
22. Orders created during a Shift belong to that Shift's operational context.

### Order

23. Orders are created from POS terminals.
24. The Order's inventory source is determined by the POS's Branch Warehouse.
25. Payment is recorded through the appropriate Wallet.
26. The Order does not directly own inventory.

---

## 14. Current Domain Model

At this stage, the core domain concepts are:

```text
Branch
Warehouse
POS
Wallet
WalletTransaction
WarehouseTransaction
Shift
User
Order
Customer
```

We deliberately do **not** introduce:

* Company entity
* Tenant entity
* POS-specific Warehouse
* CashRegister entity separate from POS
* Multi-tenancy
* Unnecessary abstractions

until an actual business requirement demands them.

---

## 15. Design Principles

### Model the Real Business

> **Model the real business, not the database.**

Every entity should exist because it represents a real business concept.

Every relationship should represent a real business relationship.

Every transaction should represent a real business event.

### Avoid Premature Abstraction

NEXUS is initially designed for one company.

We do not introduce multi-tenancy, Company entities, or other abstractions until they are required by the business.

### Transactions Are First-Class Business Events

Inventory and financial changes are not simple field updates.

They are recorded as business transactions:

```text
Warehouse
   └── Inventory Transactions

Wallet
   └── Financial Transactions
```

This provides traceability, auditability, and a reliable history of business operations.

### POS Is the Sales Boundary

The POS is the actual sales point and Cash Register.

It connects:

```text
POS
├── Branch
├── Branch Warehouse
├── Wallet
├── Active Shift
├── Salesman
├── Customer
└── Orders
```

This makes the POS the central operational boundary for the retail sales flow.

---

## 16. NEXUS Core Concept

The current NEXUS business model can be summarized as:

```text
                         NEXUS
                           │
              ┌────────────┼────────────┐
              │            │            │
           Branches     Warehouses     Wallets
              │
              ▼
           Branch
        ┌─────┼──────┐
        │     │      │
   Warehouse POS   Wallet
             │
       ┌─────┼─────┐
       │     │     │
    Wallet Shift  Orders
             │
          Salesman
             │
          Customer
```

The fundamental retail operation is:

```text
Salesman
    │
    ▼
   POS
    │
    ├── creates Order
    │
    ├── uses Branch Warehouse
    │       └── Inventory OUT
    │
    ├── uses POS Wallet
    │       └── Financial INCOME
    │
    └── operates inside a Shift
```

This model is the current baseline for NEXUS Phase 0 — Planning.

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

# 2. Business Structure

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
    ├── POS / Cash Register Wallets
    └── ...
```

---

# 3. Branches

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

### Branch Rule

> Every Branch MUST have exactly one Warehouse.

The Branch Warehouse is the inventory source used by all POS terminals belonging to that Branch.

---

# 4. Warehouses

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

Warehouse stock changes only through inventory transactions:

```text
Warehouse
│
└── Transactions
    ├── IN
    ├── OUT
    └── TRANSFER
```

### Examples

Receiving stock:

```text
Supplier
   │
   ▼
Warehouse
   │
   └── IN
```

Transferring stock:

```text
Central Warehouse
        │
        │ TRANSFER
        ▼
Branch A Warehouse
```

Selling stock:

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

The Order itself does not directly own inventory.

The resulting inventory movement is recorded as a Warehouse transaction.

---

# 5. POS — Point of Sale

A **POS** represents an actual sales point inside a Branch.

```text
Branch A
│
├── Warehouse A
│
├── POS A1
├── POS A2
└── POS A3
```

A POS:

* Belongs to exactly one Branch.
* Creates Orders.
* Uses the Warehouse of its Branch automatically.
* Has authorized users.
* Operates through Work Shifts.
* Is associated with a Cash Register / financial wallet.

### Important Rule

> A POS does NOT have its own Warehouse.

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

---

# 6. Orders

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
* Which financial wallet receives the payment.

---

# 7. Wallets

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
* Cash Register Wallet
* POS Wallet
* Other financial wallets as required

---

# 8. Branch Wallet

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

For example:

```text
POS Cash Register
       │
       │ TRANSFER
       ▼
Branch Wallet
```

---

# 9. Cash Register

A Cash Register represents the cash-handling point associated with a POS.

Each Cash Register has a Wallet.

```text
POS
│
└── Cash Register
     │
     └── Wallet
```

The Cash Register Wallet records financial movements resulting from sales and other cash operations.

---

# 10. Work Shifts

Sales operations at a Cash Register are organized into **Work Shifts**.

A Shift represents a period during which a Sales Employee is responsible for a Cash Register.

```text
Cash Register
│
└── Shifts
    ├── Shift #001 → Salesman A
    ├── Shift #002 → Salesman B
    └── ...
```

### Shift Rule

> A Cash Register can have only one active Shift at a time.

A Shift belongs to one Sales Employee.

The Shift provides the operational context for Orders and cash movements.

---

# 11. Users & Permissions

Users are not owned by a POS or Cash Register.

Instead, users are assigned permissions and operational access.

For example:

```text
User
│
├── Role
└── Permissions
```

Possible permissions include:

```text
VIEW_INVENTORY
CREATE_ORDER
OPEN_SHIFT
CLOSE_SHIFT
VIEW_SALES
...
```

A Sales Employee may be authorized to use a specific Cash Register/POS during a Shift.

---

# 12. Core Business Flow

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
          │         Cash Register
          │              │
          │              ▼
          │            Wallet
          │
          └──────────────┘
```

---

# 13. Fundamental Relationships

The current NEXUS model can be summarized as:

```text
NEXUS
│
├── Branches
│   │
│   ├── Warehouse (1)
│   │
│   ├── POS (N)
│   │    │
│   │    ├── Cash Register
│   │    │     └── Wallet
│   │    │
│   │    └── Users / Shifts
│   │
│   └── Wallet (1)
│
├── Warehouses
│   └── Inventory Transactions
│
└── Wallets
    └── Financial Transactions
```

---

# 14. Core Business Rules

The initial NEXUS model establishes the following rules:

### Branch

1. NEXUS has many Branches.
2. Every Branch has exactly one Warehouse.
3. Every Branch has one Branch Wallet.
4. A Branch can have many POS terminals.

### POS

5. Every POS belongs to exactly one Branch.
6. A POS does not own a Warehouse.
7. A POS automatically operates against its Branch Warehouse.
8. A POS creates Orders.
9. A POS operates through a Cash Register.

### Warehouse

10. NEXUS can have many Warehouses.
11. A Warehouse records inventory transactions.
12. Inventory movements are represented by IN, OUT, and TRANSFER operations.

### Wallet

13. NEXUS can have many Wallets.
14. Branches have Wallets.
15. Cash Registers have Wallets.
16. Wallets record INCOME, OUTCOME, and TRANSFER transactions.

### Shift

17. A Cash Register can have only one active Shift.
18. A Shift is assigned to one Sales Employee.
19. Orders created during a Shift belong to its operational context.

### Order

20. Orders are created from POS terminals.
21. The Order's inventory source is determined by the POS's Branch Warehouse.
22. Payment is recorded through the appropriate Wallet.

---

# 15. Current Domain Model

At this stage, the core domain entities are:

```text
Branch
Warehouse
POS
CashRegister
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
* Multi-tenancy
* Unnecessary abstractions

until an actual business requirement demands them.

---

# 16. NEXUS Design Principle

The core design principle of NEXUS is:

> **Model the real business, not the database.**

Every entity should exist because it represents a real business concept.

Every relationship should represent a real business relationship.

Every transaction should represent a real business event.

The architecture should emerge from these rules rather than forcing the business into predefined technical abstractions.

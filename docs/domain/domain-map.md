# NEXUS — Domain Map

> This is a Domain Discovery snapshot, not the final Domain Model.

## 1. Current Domain Landscape

```text
NEXUS
│
├── Branch
│   ├── POS
│   │   ├── Wallet
│   │   └── Shifts
│   │
│   ├── Warehouse
│   │
│   └── Branch Financial Context
│
├── User
│   ├── Role
│   ├── Permissions
│   └── POS Assignments
│
├── Customer
│   ├── Takeaway Context
│   ├── Identified Customer
│   └── Customer Grade
│
├── Sale
│   ├── Customer Context
│   ├── Products / Items
│   ├── Payment
│   └── Financial Effects
│
└── Return
```

---

## 2. Branch

Branch represents an independent operational unit.

A Branch is associated with:

* POSes
* One Warehouse
* Branch financial context

POSes and Warehouses cannot move between Branches.

Users are not exclusively owned by a Branch.

---

## 3. POS

A POS is an operational sales point belonging to a Branch.

A POS has:

* Wallet
* Shifts

A POS performs:

* Sales
* Returns

A POS does not perform Purchases.

---

## 4. User

A User authenticates into NEXUS and receives functionality according to Role and Permissions.

A User may operate across multiple Branches.

A User may be assigned to multiple POSes.

POS assignments can include sales eligibility.

---

## 5. Shift

A Shift represents an operational and financial period for a POS.

Current understanding:

```text
Shift
├── Salesman: 1
└── Managers: 1..n
```

A Shift participates in the POS financial lifecycle.

Its closing process can use:

* Settlement
* REMAIN

---

## 6. Wallet

The current domain contains at least:

* POS Wallet
* Branch Wallet

A Sale's actually received amount affects the POS Wallet.

A confirmed settlement transfers an amount from POS Wallet to Branch Wallet.

---

## 7. Customer

Customer has two broad contexts:

```text
Customer
├── Online Customer        [Deferred]
│
└── Insite Customer
    ├── Takeaway
    └── Identified Customer
```

An Identified Customer has a Customer record.

An Identified Customer may have a receivable/debt.

---

## 8. Customer Grade

Existing customers have a grade:

```text
Blocked
Normal
Premium
VIP
```

The grade is operational information used during the sales process.

---

## 9. Sale

A Sale connects several domain concepts:

```text
Sale
├── POS
├── Shift
├── Customer Context
├── Products / Items
├── Payment
├── Inventory Effect
└── Financial Effects
```

A Sale can result in:

* Stock reduction
* POS Wallet increase for the received amount
* Customer receivable for an unpaid amount

---

## 10. Return

A Return is a physical POS operation that can increase stock in the Branch Warehouse.

The detailed Return model remains under discovery.

---

## 11. Important Relationships

```text
Branch ─────── POS
Branch ─────── Warehouse

POS ────────── Wallet
POS ────────── Shift

User ───────── POS Assignment
User ───────── Branch Access

Shift ──────── Salesman
Shift ──────── Manager(s)

Sale ───────── POS
Sale ───────── Shift
Sale ───────── Customer Context
Sale ───────── Product Items

Sale ───────── Warehouse Effect
Sale ───────── Wallet Effect
Sale ───────── Customer Receivable
```

---

## 12. Deliberately Unresolved

The following relationships are not finalized:

* Exact ownership semantics for Wallets.
* Exact relationship between Shift and Wallet.
* Whether Customer Receivable is a standalone Domain Entity.
* Exact Sale aggregate boundary.
* Exact Inventory aggregate boundary.
* Exact relationship between Sale and Stock Transaction.
* Exact Return relationship to the original Sale.
* Exact User/Role/Permission model.

---
## Inventory

Category
  |
  +-- Attribute Definitions
  |
  +-- Subcategory
        |
        +-- inherited Attribute Definitions
        +-- additional Attribute Definitions
        |
        +-- Product
              |
              +-- inherited Attribute Definitions
              +-- Product-specific Attribute Definitions
              +-- Allowed Attribute Values
              |
              +-- Primary Variant
              |
              +-- Actual Variants
                    |
                    +-- Variant Attribute Values
                    |
                    +-- Stock
                          |
                          +-- Warehouse

## Product / Variant

Product
   |
   +-- Primary Variant
   |
   +-- Actual Variant
   +-- Actual Variant
   +-- Actual Variant

* The Product itself does not hold direct Stock.
* The Primary Variant is a real Variant.
* Additional Variants are created only when actually required.

## Attribute Inheritance

Category
    ↓
Subcategory
    ↓
Product
    ↓
Variant

### Inheritance is additive.

* Category defines the base Attribute set.
* Subcategory inherits and may add.
* Product inherits and may add.
* Variant cannot introduce an Attribute outside Product Attributes.

## Stock

Warehouse
   |
   +-- Variant A → Stock
   +-- Variant B → Stock
   +-- Variant C → Stock

* Stock represents current physical quantity.
* Reserved, Damaged, and Expired are not Stock Details.
* Wastage/Loss is a separate future business concept.

  

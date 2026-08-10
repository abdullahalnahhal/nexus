# NEXUS — Vision

## 1. Purpose

NEXUS is a business management system designed around the operational reality of a physical retail business.

The initial scope focuses on the **physical retail operation**, including:

* Branches
* POS operations
* Warehouses
* Sales
* Returns
* Shifts
* Wallets
* Customers
* Customer receivables

Online operations are intentionally deferred until the physical NEXUS domain is understood and modeled.

---

## 2. Core Vision

NEXUS should model the business rather than merely provide CRUD screens.

The system should make important business concepts, rules, responsibilities, and financial consequences explicit.

The intended design direction is:

**Business Understanding → Domain Model → Architecture → Implementation**

rather than starting from database tables or framework structures.

---

## 3. Business Structure

A Branch represents an independent operational unit of the business.

A Branch may contain:

* POS terminals
* One Branch Warehouse
* Branch Wallet
* Operational users/assignments

A POS belongs to exactly one Branch.

A Warehouse belongs to exactly one Branch.

POSes and Warehouses are not transferable between Branches.

---

## 4. Users and Operational Access

Users authenticate into NEXUS first.

After authentication, the system determines the user's:

* Role
* Permissions
* Available functionality

A user may operate across multiple Branches.

A user may also be assigned to one or more POSes.

POS assignment determines whether the user is allowed to perform sales operations on that POS.

A Salesman selects an assigned POS after logging into NEXUS before starting POS operations.

---

## 5. POS

A POS is a business entity representing an operational sales point.

A POS:

* Belongs to one Branch.
* Has its own Wallet.
* Has multiple Shifts over time.
* Performs Sales.
* Performs Returns.
* Does not perform Purchase operations.
* Operates against its Branch Warehouse.

The POS itself is not the Warehouse and does not own the Branch's inventory.

---

## 6. Shifts

A Shift represents an operational and financial period associated with a POS.

A Shift includes assigned operational users.

Current business understanding:

* One Salesman participates in a Shift.
* One or more Managers may participate in a Shift.
* A Salesman cannot operate two POSes simultaneously within the same Shift context.
* A Manager may participate in multiple POSes within the same Shift.

A new Shift cannot begin until the previous Shift has completed its required confirmation/closing process.

A Shift may end through:

1. Settlement to the Branch Wallet.
2. REMAIN, where the POS balance continues into the next Shift.

---

## 7. Customers

The Customer domain currently contains two major contexts:

### Online Customer

Online Customer operations are intentionally deferred.

They will be modeled after the physical NEXUS domain is completed.

### Insite Customer

An Insite Customer can be:

* Takeaway
* Identified/registered customer

A Takeaway customer does not require a stored customer profile.

An identified customer has a customer record and can have an outstanding financial balance.

---

## 8. Customer Grade

Existing customers have a grade:

* Blocked
* Normal
* Premium
* VIP

A Blocked customer cannot make a sale until the block is removed.

The Salesman needs the customer's grade as operational information during the sales process.

---

## 9. Physical Sales

A physical Sale follows the general flow:

```text
Authenticate User
        ↓
Resolve Role & Permissions
        ↓
Select Assigned POS
        ↓
Start Sale
        ↓
Select Customer Context
        ↓
Select Products
        ↓
Determine Payment
        ↓
Apply Inventory Effect
        ↓
Apply Financial Effects
        ↓
Complete Sale
```

A Takeaway Sale must be fully paid.

An identified customer may pay the full amount or leave an outstanding amount.

Current payment methods:

* Cash
* Visa

---

## 10. Financial Effects of a Sale

For a partially paid Sale:

```text
Sale Total = X
Paid       = Y
Remaining  = Z
```

where:

```text
X = Y + Z
```

The paid amount affects the POS Wallet.

The remaining amount is recorded as a financial receivable/debt against the customer for the Branch.

The remaining amount is not treated as physical cash already present in the Branch Wallet.

---

## 11. Shift Closing

### Branch Settlement

When the POS balance is transferred to the Branch Wallet:

```text
POS Wallet
    ↓
Branch Wallet
```

The Branch Manager must confirm that the amount was received.

After confirmation:

```text
POS Wallet   -X
Branch Wallet +X
```

### REMAIN

Instead of transferring the balance to the Branch Wallet, the amount may remain associated with the POS for the next Shift.

The incoming Manager or Salesman must confirm receipt.

After confirmation, the carried amount continues into the next Shift's POS financial context.

---

## 12. Scope Boundary

### Current Scope

The initial physical NEXUS domain includes:

* Branch
* Warehouse
* POS
* Shift
* User
* Roles/Permissions
* POS Assignment
* Sale
* Return
* Customer
* Customer Grade
* POS Wallet
* Branch Wallet
* Customer Receivables

### Deferred

Online Customer operations and their dedicated Warehouse are intentionally deferred.

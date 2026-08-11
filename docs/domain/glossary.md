# NEXUS — Domain Glossary

> Terms in this document represent the current business language of NEXUS.

## Branch

An independent operational unit of the physical business.

A Branch has its own POSes, Warehouse, and Branch financial context.

---

## POS

The operational sales point used by the Branch.

A POS has its own Wallet and operates through Shifts.

In physical NEXUS, a POS performs Sales and Returns but does not perform Purchases.

---

## Warehouse

The inventory location associated with a Branch.

Each Branch has its own Warehouse.

A Warehouse cannot be transferred between Branches.

---

## Shift

An operational and financial period associated with a POS.

A Shift has one Salesman and may have multiple Managers.

A Shift must complete its closing/confirmation process before another Shift can start on the same POS.

---

## POS Wallet

The financial balance associated with a POS.

It is affected by amounts actually received through POS operations and by confirmed financial transfers.

---

## Branch Wallet

The Branch-level cash wallet.

A confirmed POS settlement increases the Branch Wallet and decreases the POS Wallet by the same amount.

---

## Sale

A physical retail transaction performed through a POS.

A Sale contains selected products and quantities and produces inventory and financial effects.

---

## Return

A physical POS operation that returns previously sold goods and can increase Branch Warehouse stock.

The detailed Return lifecycle is still under discovery.

---

## Takeaway Customer

An Insite customer context where the customer does not have a stored customer profile.

A Takeaway Sale must be fully paid.

---

## Identified Customer

An Insite customer who has an existing customer record or chooses to register one.

An Identified Customer may have an outstanding receivable.

---

## Online Customer

A customer operating through the future online sales domain.

Online Customer functionality is currently deferred.

---

## Customer Grade

The business classification of an existing customer.

Current grades:

* Blocked
* Normal
* Premium
* VIP

---

## Blocked Customer

A customer who cannot make a Sale until the block is removed.

---

## Customer Receivable

An amount owed by a customer to the Branch as a result of an unpaid portion of a Sale.

A receivable is not the same as cash physically held in the Branch Wallet.

---

## REMAIN

The process of carrying the POS financial balance from one Shift into the next instead of settling it into the Branch Wallet.

REMAIN requires confirmation by the incoming Manager or Salesman.

---

## Settlement

The process of transferring the POS financial balance to the Branch Wallet at the end of a Shift.

Branch Manager confirmation is required.

---

## POS Assignment

The relationship that determines which POSes a User may operate.

A POS Assignment may also determine whether the User is permitted to perform Sales operations on that POS.

---

## Salesman

A User role involved in performing physical Sales through a POS.

A Salesman operates within a Shift and cannot simultaneously operate two POSes within the same Shift context.

---

## Manager

A User role involved in supervising POS operations and performing management responsibilities.

A Manager may participate in multiple POSes within the same Shift.

---

## Insite Customer

A customer context belonging to the physical retail operation.

It currently includes:

* Takeaway
* Identified Customer

--- 

## Inventory Terms

### Category
A business classification level used to organize Products and define reusable Attribute Definitions.

### Subcategory
An optional child classification of a Category.

### Product
The business-level product concept.

A Product does not have direct Stock.

### Variant
A concrete configuration of a Product distinguished by Variant-Defining Attribute values.

> `Variant` is the agreed term. `Alternative` is no longer used.

### Primary Variant
The automatically-created base Variant of a Product.

### Attribute Definition
A reusable definition describing a Product characteristic.

### Attribute Value
The actual value assigned to an Attribute.

### Variant-Defining Attribute
An Attribute whose value participates in identifying a Variant.

### Stock
The current physical quantity of a Product Variant in a Warehouse.

### Wastage / Loss
A separate business event in which Stock is written off or removed for a reason such as damage or expiry.

### Stock Movement
A future domain concept representing a business change to Stock.

### Stock Details
Not a current NEXUS domain concept.

Reserved/Damaged/Expired are intentionally not modeled as Stock Details.

## Attribute Types

- TEXT
- NUMBER
- DATE
- SELECT
- MULTI_SELECT
- BOOLEAN
---

## New Terms — Phase 0.2

### Supplier Company

The company from which NEXUS purchases goods.

A Supplier Company may have multiple Supplier Branches and has the actual financial liability relationship with NEXUS.

---

### Supplier Branch

A specific operational branch of a Supplier Company.

The Supplier Branch owns its:

- Reference Person
- Manager
- Representative(s)

---

### Supplier Representative

A representative associated with a Supplier Branch.

A Representative may be attributed a portion of the Supplier Company's outstanding amount.

The attributed amount is not an independent financial liability.

---

### Supplier Opening Balance

The financial balance existing for a Supplier Company when it is introduced into NEXUS.

---

### Purchase Invoice

The NEXUS document representing both the purchase transaction and the receipt of the purchased goods.

Purchase Invoice and Goods Receipt are the same business document in NEXUS.

---

### Supplier Return Invoice

A financial and inventory document used when goods are returned to a Supplier.

Its return value does not necessarily equal the original purchase value.

---

### Supplier Return Settlement

The financial treatment specified by a Supplier Return Invoice.

Current discovered examples include:

- Cash received
- Set-off / Offset

---

### Replacement Document

A separate document representing the replacement of returned goods with new goods.

Replacement is intentionally outside the current Supplier Return scope.

---

### Supplier Payment

A financial transaction used to pay a Supplier-related financial obligation.

A Supplier Payment can be allocated across multiple Purchase Invoices or Supplier Receipts.

---

### Payment Allocation

The portion of a Supplier Payment assigned to a specific financial document.

---

### Payment Destination

The financial destination receiving a Supplier Payment.

It may represent a Supplier-related account/company and does not necessarily equal the Supplier Company record used on the Purchase Invoice.

---

### Supplier Receipt

A Supplier-related financial document that may receive an allocation from a Supplier Payment.

The exact business definition and lifecycle remain under discovery.

---

### Main Warehouse

The Warehouse from which Branch Sales are performed.

---

### Secondary Warehouse

A Warehouse that is not the Main Warehouse of a Branch.

Secondary Warehouses cannot be used directly for Sales.

---

### Independent Warehouse

A Warehouse that is not required to belong to a Branch.

An Independent Warehouse may participate in Inventory operations such as Transfers.

---

### Stock Movement

A historical business event explaining a change in Stock.

Current discovered movement names:

```text
Download - Buy
Upload - Sell
Upload - Transfer
Download - Transfer
Upload - Supplier Returns
Download - Customer Return
Damage
Miss
Manual Edit
```
---

### Manual Edit

A Stock adjustment that may increase or decrease Stock.

It requires Warehouse Manager approval before it becomes effective.

---

### Debt Attribution

A subdivision of the Supplier Company's actual financial liability among operational dimensions such as Supplier Branch or Representative.

Debt attribution does not create an independent liability.

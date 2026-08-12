# NEXUS — Business Story

## 1. The Business

NEXUS models a retail business operating through independent physical Branches.

Each Branch operates as a business unit with its own operational environment.

A typical Branch contains:

```text
Branch
├── POSes
├── Warehouse
└── Branch Wallet
```

Users operate within this environment according to their roles, permissions, and POS assignments.

---

## 2. A User Enters NEXUS

A user first authenticates into NEXUS.

NEXUS determines the user's role and permissions and exposes the functionality available to that user.

If the user has POS-related access, they can select from the POSes to which they are assigned.

A Salesman can only sell on a POS where the assignment allows sales operations.

---

## 3. Starting a Sale

The Salesman starts a new Sale from the selected POS.

The first business decision is the customer context.

The customer may be:

### Takeaway

The customer does not have a stored profile.

The Sale must be fully paid.

### Identified Customer

The customer already exists or chooses to register.

The customer has a Customer record and may have an outstanding balance.

If an existing customer is Blocked, the Sale cannot proceed until the block is removed.

---

## 4. Selecting Products

The Salesman selects products through the POS interface.

Products may be navigated through categories and subcategories or searched directly.

The selected products and quantities form the Sale's current basket/cart.

The exact inventory availability rules are still under discovery.

---

## 5. Payment

The current physical payment methods are:

* Cash
* Visa

For a Takeaway customer:

```text
Total = Paid
Remaining = 0
```

For an identified customer:

```text
Total = Paid + Remaining
```

The customer may therefore leave part of the Sale as an outstanding amount.

---

## 6. Financial Consequences

Suppose:

```text
Sale Total = 1,000
Paid       = 700
Remaining  = 300
```

The business consequences are:

```text
POS Wallet
+700
```

and:

```text
Customer Receivable
+300
```

The Branch therefore has a financial claim of 300 against the customer.

The 300 is not treated as cash physically received by the Branch.

---

## 7. Inventory Consequences

A Sale affects the Branch Warehouse.

The current understanding is that the Sale causes the sold stock to leave the Branch Warehouse.

The exact timing and validation rules for inventory deduction remain part of the ongoing Domain Discovery.

---

## 8. Shift Closing

At the end of a Shift, the POS's financial balance must be dealt with before another Shift can start.

There are two known paths.

### Settlement

The amount is transferred from the POS Wallet to the Branch Wallet.

The Branch Manager confirms receipt.

### REMAIN

The amount stays associated with the POS and continues into the next Shift.

The incoming Manager or Salesman confirms receipt.

---

## 9. Returns

A POS can perform Returns.

A Return can increase the Branch Warehouse inventory.

A POS does not perform Purchase operations.

The exact Return workflow and its relationship to the original Sale remain part of the Domain Discovery.

---

## 10. Future Online Domain

NEXUS will eventually support Online Customers.

Online Customers will operate against a dedicated Online Warehouse.

This domain is intentionally deferred until the physical NEXUS domain is completed.

---

## Phase 0.2 — Inventory Discovery Update

The Inventory story was extended with the following confirmed behavior.

Products are classified through Categories and optional Subcategories. Categories can define reusable Attribute Definitions. Subcategories inherit those definitions and may add new ones. Products inherit the resulting definitions and may add Product-specific Attributes.

A Product automatically receives exactly one Primary Variant. The Primary Variant is a real Variant and can carry stock. Additional Variants are created only when the business actually needs them. The system does not generate all possible combinations of Attribute values.

A Variant uses only Product Attributes. Variant-defining Attribute values identify the Variant, and the same complete combination cannot be duplicated within one Product.

Stock is maintained per Product Variant in a Warehouse. Stock is the current physical quantity. We intentionally removed Reserved, Damaged, and Expired as Stock Detail buckets.

When goods are damaged, expired, or otherwise written off, the quantity is reduced and the reason belongs to a separate future Wastage/Loss or Stock Movement concept.

This section records business discoveries only; implementation details remain open.

---

## Phase 0.2 — Stock Adjustment Discovery Synchronization

A Stock Adjustment is an independent Inventory business document used to correct Stock for an allowed business reason.

A user may create it manually when the user has the required Permission and the reason is allowed. No additional Approval step is required for Stock Adjustment.

The business flow is:

```text
Allowed Reason + Required Permission
              ↓
      Issue Stock Adjustment
              ↓
       Immediate Stock Effect
```

The same Product may appear on multiple Adjustment lines; the resulting Stock effect uses the aggregate quantity for that Product.

Reason/Reference is sufficient for traceability in the current scope. Attachments are not required.

After issuance, the Stock Adjustment cannot be edited or cancelled. It has no accounting effect, and no separate document reference-number requirement is introduced in the current phase.

UOM and costing are deliberately deferred.
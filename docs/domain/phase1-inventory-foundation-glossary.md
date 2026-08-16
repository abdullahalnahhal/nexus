# NEXUS — Glossary

| Term | Definition |
|---|---|
| Product | An item managed by NEXUS inventory. |
| Warehouse | A physical/logical inventory location that participates in inventory transactions. |
| Product-Warehouse Setup | The configuration/relationship enabling a Product to be managed in a Warehouse. |
| Current Stock | The current quantity state for one Product + Warehouse. It is the Source of Truth for current quantity. |
| Stock Movement | An immutable inventory effect representing quantity moving IN or OUT for a Product + Warehouse. |
| Inventory Document | A business transaction/document that gives meaning and origin to an inventory effect. |
| Inventory Operation | A business operation such as Sale, Purchase, Return, Transfer, Adjustment, Loss, Depreciation, or Opening Balance. |
| IN Movement | A Stock Movement that increases Current Stock. |
| OUT Movement | A Stock Movement that decreases Current Stock. |
| Transfer | A warehouse-to-warehouse inventory operation producing an OUT movement and an IN movement atomically. |
| Stock Adjustment | A controlled inventory document used to correct/reconcile inventory according to permissions and approval rules. |
| Source of Truth | The authoritative representation of the current inventory quantity. In NEXUS this is Current Stock. |
| Immutable | Once created, the record cannot be modified or deleted as a correction mechanism. |
| Reserved Stock | A separate quantity held against future demand. NEXUS does not currently model this. |
| Inventory Identity | The dimensions that determine which stock record a quantity belongs to. Currently Product + Warehouse. |
| Cost | Monetary purchase/transaction value stored on relevant documents/invoices; not carried by Stock Movement in the current phase. |
| Approval | A controlled lifecycle action required for applicable inventory operations. |
| Permission | The authorization unit used by NEXUS instead of a hardcoded Manager role. |

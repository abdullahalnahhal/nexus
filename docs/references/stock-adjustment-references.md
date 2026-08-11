# NEXUS — Stock Adjustment References

## Phase 0.2 Inventory Discovery — Checkpoint 0.2-A

### 1. SAP Business ByDesign — Create an Inventory Adjustment

urlSAP Help — Create an Inventory Adjustmenthttps://help.sap.com/docs/SAP_BUSINESS_BYDESIGN/2754875d2d2a403f95e58a41a9c7d6de/2d8f753f722d1014996d8458a29da513.html

**What we learned:** Inventory adjustments are treated as explicit warehouse/product operations and are used to correct inventory quantities when the system record no longer represents the physical situation. This supports modeling Adjustment as a business document rather than as an unrestricted stock edit.

### 2. Odoo — Inventory Adjustments

urlOdoo Inventory Adjustments documentationhttps://www.odoo.com/documentation/master/applications/inventory_and_mrp/inventory/warehouses_storage/inventory_management/count_products.html

**What we learned:** Odoo explicitly associates an inventory adjustment with a reason/reference and records the resulting stock move in movement history for traceability. This supports NEXUS requiring Reason/Reference as part of the Adjustment record.

### 3. Shopify — Inventory adjustment reasons

urlShopify inventory adjustment documentationhttps://help.shopify.com/en/manual/products/inventory/adjusting-inventory/adjusting-inventory-quantities

**What we learned:** Inventory quantity changes are accompanied by reasons such as correction and count, reinforcing the NEXUS rule that a stock change should have a business reason rather than being an unexplained quantity mutation.

### 4. Zoho ERP — Inventory Adjustments

urlZoho ERP inventory adjustment documentationhttps://www.zoho.com/en-in/erp/kb/inventory/inventory-adjustments/how-to-adjust-stock.html

**What we learned:** Inventory adjustment workflows commonly identify the location/warehouse, adjustment mode, reason, and affected items. This supports the NEXUS separation between warehouse scope, reason, and inventory lines.

### 5. Inventory Record Inaccuracy research

Rekik, Y., Oliva, R., Glock, C. H., & Syntetos, A. — *Inventory record inaccuracy in grocery retailing: Impact of promotions and product perishability, and targeted effect of audits* (2025).

urlResearch paper on inventory record inaccuracyhttps://arxiv.org/abs/2506.05357

**What we learned:** Inventory record inaccuracies are a real operational problem and physical audits can have measurable business impact. This provides academic context for treating inventory correction as a controlled, traceable business process.

### Reference boundary

These references inform the domain discovery only. They do not dictate NEXUS implementation or override decisions made during the NEXUS discovery process.

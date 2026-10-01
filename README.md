# 📊 Data Modeling in Power BI

<div align="center">

![Power BI](https://img.shields.io/badge/Power%20BI-Semantic%20Model-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Power Query](https://img.shields.io/badge/Power%20Query-Data%20Transformation-217346?style=for-the-badge&logo=microsoft-excel&logoColor=white)
![DAX](https://img.shields.io/badge/DAX-Business%20Measures-5B2C6F?style=for-the-badge)
![Status](https://img.shields.io/badge/Project-Completed-28A745?style=for-the-badge)

### From disconnected operational tables to a governed, analysis-ready dimensional model

**Reliable numbers · Faster report development · Reusable dimensions · Regional data security**

[Download the Power BI project](power-bi/Power_BI_Data_Modeling_Project.pbix) · [View the final model](assets/power-bi-after-modeling.png)

</div>

---

## 🎯 Executive summary

| Business problem | Solution delivered | Business value |
|---|---|---|
| Sales, orders, invoices, inventory, campaigns, and customer data were fragmented across inconsistent source tables. | Redesigned the data as a governed dimensional model with shared dimensions, controlled relationships, reusable DAX measures, and row-level security. | Users receive trusted metrics, analysts build reports faster, and BI teams gain a model that is easier to test, secure, maintain, and extend. |

### At a glance

| ⭐ Model | 📈 Analysis | 🔐 Governance | ✅ Quality |
|---|---|---|---|
| **6 dimensions** and **6 fact tables** | Sales, orders, inventory, campaigns, promotions, and targets | Dynamic regional row-level security | Grain, totals, cardinality, and filter paths validated |

---

## 🔄 Transformation: before → after

| ❌ Before — disconnected source tables | ✅ After — governed dimensional model |
|---|---|
| Inconsistent names, duplicated entities, mixed grains, and no dependable relationship structure | Reusable dimensions, clearly defined facts, one-to-many relationships, and controlled filter direction |
| ![Power BI model before data modeling](assets/power-bi-before-modeling.png) | ![Power BI model after data modeling](assets/power-bi-after-modeling.png) |

<details>
<summary><strong>View the illustrated architecture comparison</strong></summary>

### Raw source landscape

![Raw tables before modeling](assets/before-data-modeling.png)

### Final semantic model

![Dimensional model after modeling](assets/after-data-modeling.png)

</details>

---

## 💼 The business challenge

The source structure made even basic questions difficult to answer confidently:

- Are sales totals correct, or are relationships duplicating transactions?
- How many customers are actively ordering?
- How long does an order take to move from placement to payment?
- Are campaigns producing engagement across the intended products?
- How do actual sales compare with monthly targets?
- Can regional users be restricted to only the data they are authorized to see?

### Risks in the original model

| Risk | Business impact |
|---|---|
| **Mixed table grains** | Incorrect totals and silent duplication |
| **Disconnected and duplicated entities** | Conflicting customer, product, and location views |
| **Technical and inconsistent naming** | Slow report development and difficult handover |
| **Uncontrolled filter paths** | Ambiguous calculations and unpredictable reports |
| **No governed security layer** | Users could receive inappropriate regional visibility |

---

## 💡 The solution

```text
Raw operational tables
        ↓
Power Query cleanup and consolidation
        ↓
Conformed dimensions + business-process facts
        ↓
Governed relationships + reusable DAX measures
        ↓
Validated, secure semantic model for reporting
```

| What was built | Why it matters |
|---|---|
| **Clearly defined fact-table grains** | Protects totals and prevents accidental duplication |
| **Shared customer, product, date, geography, campaign, and order dimensions** | Creates consistent slicing across business processes |
| **Single-direction, one-to-many relationships** | Produces predictable filter behavior |
| **Surrogate keys and `snake_case` naming** | Improves consistency, readability, and maintainability |
| **Centralized DAX measures** | Gives every report the same business logic |
| **Dynamic regional row-level security** | Restricts data based on the signed-in user |
| **Incremental validation checks** | Detects broken totals before changes reach reports |

---

## 🏗️ Model architecture

| Dimensions | Business purpose |
|---|---|
| `dim_customer` | Customer, account, contact, location, and payment context |
| `dim_product` | Product, brand, category, supplier, and pricing context |
| `dim_date` | Shared calendar for consistent time analysis |
| `dim_geo` | Reusable city and region mapping |
| `dim_campaign` | Campaign, channel, budget, and schedule context |
| `dim_order_flag` | Order channel and priority classification |

| Facts | Grain / analytical purpose |
|---|---|
| `fact_sales` | One row per order line; sales, quantity, cost, and discount analysis |
| `fact_order_process` | One row per order; lifecycle from order through payment |
| `fact_inventory` | Monthly units by product |
| `fact_campaign` | Daily campaign clicks, impressions, and spend |
| `fact_promotion_coverage` | Campaign-to-product promotion coverage |
| `fact_sales_target` | Revenue target by date |

> `security` maps users to regions and propagates authorized access through `dim_customer` to the relevant facts.

---

## 👥 How it helps users

| Audience | Outcome |
|---|---|
| **Business users** | Explore trusted sales, customer, product, inventory, campaign, and target metrics without understanding source-system complexity. |
| **Analysts & report developers** | Build visuals faster using friendly dimensions and reusable measures instead of rebuilding joins and calculations. |
| **Managers** | Compare actuals with targets and monitor the complete order-to-payment lifecycle from one model. |
| **BI & data teams** | Refresh, test, troubleshoot, secure, extend, and hand over the model more confidently. |

---

## ✅ Validation & governance

- Verified row counts and declared the grain of every fact.
- Used distinct-order checks where the physical table grain is order line.
- Reviewed relationship cardinality and filter direction.
- Reconciled business totals after each major transformation.
- Retained only intentional inactive date and geography relationships.
- Tested regional security with representative users.

---

## 🧰 Skills demonstrated

| Modeling & BI | Transformation & logic | Quality & governance |
|---|---|---|
| Power BI · Dimensional modeling · Star schema design | Power Query · DAX · Surrogate keys | Data validation · Relationship design · Row-level security |

---

## 🚀 Explore the project

1. Download [`Power_BI_Data_Modeling_Project.pbix`](power-bi/Power_BI_Data_Modeling_Project.pbix).
2. Open it in **Power BI Desktop**.
3. Review the Power Query transformations, model relationships, measures, and security role.

```text
Data_Modeling-in-Power-BI/
├── assets/     # Real Power BI screenshots and architecture diagrams
├── power-bi/   # Completed PBIX project
└── README.md
```

> The repository contains the completed Power BI file and model documentation. Original raw data files are intentionally excluded.

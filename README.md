# Data Modeling in Power BI

A portfolio project demonstrating how a disconnected, inconsistent collection of operational tables can be transformed into a clean dimensional model in Power BI.

The project focuses on model design rather than dashboard styling: defining table grain, separating facts from dimensions, standardizing names, controlling filter direction, validating totals, and applying regional row-level security.

## From business problem to solution

### The business problem

The organization had sales, orders, invoices, payments, shipments, inventory, campaigns, targets, customers, and products spread across disconnected operational tables. Several tables described the same business entities in different ways, yearly order data was separated, column names were inconsistent, and reporting attributes were mixed into transaction tables.

This structure created three major business risks:

- **Unreliable reporting:** ambiguous relationships and mismatched table grains could duplicate records or produce incorrect totals.
- **Slow development and performance:** analysts had to repeatedly interpret technical source tables, while unnecessary columns increased model size and refresh effort.
- **Poor governance:** inconsistent names, uncontrolled filter paths, and missing security rules made the model difficult to maintain and unsafe to distribute broadly.

As a result, report developers could not confidently answer basic questions such as total sales, active customers, order-processing time, campaign performance, inventory levels, or progress against revenue targets.

### The solution built

The raw structure was redesigned as a governed dimensional model in Power BI. The solution:

- Consolidates related source tables and standardizes them in Power Query.
- Separates measurable business events into clearly defined fact tables.
- Creates reusable customer, product, date, geography, campaign, and order-flag dimensions.
- Preserves the correct grain for each business process.
- Uses controlled one-to-many relationships with dimensions filtering facts.
- Centralizes reusable DAX measures for consistent calculations.
- Validates key totals throughout the transformation process.
- Applies dynamic regional row-level security so users see only the data they are authorized to access.

### How the solution helps users

**Business users** receive consistent numbers across reports and can analyze sales, customers, products, campaigns, inventory, targets, and order timelines without needing to understand the raw source systems.

**Report developers and analysts** can build visuals faster from friendly dimensions and trusted measures instead of recreating joins and calculations for every report.

**Managers** gain a reliable view of performance across multiple business processes, including actual-versus-target analysis and the time between ordering, shipping, invoicing, and payment.

**Data and BI teams** benefit from a model that is easier to refresh, test, troubleshoot, extend, secure, and hand over to other developers.

The result is a scalable semantic layer that turns fragmented operational data into trustworthy, analysis-ready information.

## Skills demonstrated

- Power BI
- Power Query
- Dimensional modeling
- Star schema design
- DAX
- Data validation
- Relationship design
- Surrogate key design
- Row-level security
- Analytics engineering

## Before and after

### Raw source structure

The starting point contains disconnected Databricks-style source tables with inconsistent naming, duplicated entities, denormalized attributes, and multiple business processes.

**Power BI model view before transformation**

![Power BI model view before data modeling](assets/power-bi-before-modeling.png)

**Conceptual view of the raw tables**

![Raw tables before modeling](assets/before-data-modeling.png)

### Final dimensional model

The completed model uses reusable dimensions and governed one-to-many relationships across sales, order processing, inventory, campaigns, promotion coverage, and sales targets.

**Power BI model view after transformation**

![Power BI model view after data modeling](assets/power-bi-after-modeling.png)

**Conceptual view of the dimensional model**

![Dimensional model after modeling](assets/after-data-modeling.png)

## Model architecture

### Dimensions

- `dim_customer` — customer, account, contact, location, and payment attributes
- `dim_product` — product, brand, category, supplier, and pricing attributes
- `dim_date` — shared calendar attributes for time-based analysis
- `dim_geo` — reusable city and region mapping
- `dim_campaign` — campaign details, channel, budget, and campaign dates
- `dim_order_flag` — channel and priority classification for orders

### Facts

- `fact_sales` — order-line sales at line-item grain
- `fact_order_process` — order lifecycle dates from order through payment
- `fact_inventory` — monthly inventory units by product
- `fact_campaign` — daily marketing performance, including spend, clicks, and impressions
- `fact_promotion_coverage` — bridge between campaigns and promoted products
- `fact_sales_target` — revenue targets by date

### Supporting table

- `security` — maps users to regions for dynamic row-level security

## Key modeling decisions

- Consolidated yearly order sources before modeling.
- Defined and preserved the grain of every fact table.
- Removed duplicate, technical, and reporting-irrelevant columns.
- Standardized table and column names with `snake_case` conventions.
- Created surrogate keys with the `_key` suffix.
- Avoided direct fact-to-fact relationships.
- Used shared dimensions to filter facts in a single direction.
- Kept only intentional inactive date/geography relationships.
- Added centralized measures for reusable business logic.
- Applied dynamic regional row-level security.

## Validation approach

Model changes were checked incrementally to prevent totals from breaking silently. Validation included:

- Row-count and grain checks after transformations
- Distinct-order checks for line-level sales
- Relationship cardinality and filter-direction review
- Comparison of business totals before and after model changes
- Role-level security testing with representative users

## Repository contents

```text
.
|-- assets/
|   |-- before-data-modeling.png
|   |-- after-data-modeling.png
|   |-- power-bi-before-modeling.png
|   `-- power-bi-after-modeling.png
|-- power-bi/
|   `-- Power_BI_Data_Modeling_Project.pbix
`-- README.md
```

## Open the project

1. Download or clone this repository.
2. Open `power-bi/Power_BI_Data_Modeling_Project.pbix` in Power BI Desktop.
3. Review the model view, Power Query transformations, measures, relationships, and security role.

> The repository includes the finished Power BI file and architecture diagrams. The original raw data files are not included.

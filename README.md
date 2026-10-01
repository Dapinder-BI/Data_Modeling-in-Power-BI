# Data Modeling in Power BI

A portfolio project demonstrating how a disconnected, inconsistent collection of operational tables can be transformed into a clean dimensional model in Power BI.

The project focuses on model design rather than dashboard styling: defining table grain, separating facts from dimensions, standardizing names, controlling filter direction, validating totals, and applying regional row-level security.

## Before and after

### Raw source structure

The starting point contains disconnected Databricks-style source tables with inconsistent naming, duplicated entities, denormalized attributes, and multiple business processes.

![Raw tables before modeling](assets/before-data-modeling.png)

### Final dimensional model

The completed model uses reusable dimensions and governed one-to-many relationships across sales, order processing, inventory, campaigns, promotion coverage, and sales targets.

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
|   `-- after-data-modeling.png
|-- power-bi/
|   `-- Power_BI_Data_Modeling_Project.pbix
`-- README.md
```

## Open the project

1. Download or clone this repository.
2. Open `power-bi/Power_BI_Data_Modeling_Project.pbix` in Power BI Desktop.
3. Review the model view, Power Query transformations, measures, relationships, and security role.

> The repository includes the finished Power BI file and architecture diagrams. The original raw data files are not included.

## Skills demonstrated

Power BI, Power Query, dimensional modeling, star schema design, DAX, data validation, relationship design, surrogate keys, role-level security, and analytics engineering.

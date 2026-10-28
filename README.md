# Critical Minerals Market Intelligence — Snowflake + Power BI

A Snowflake data warehouse with a Power BI reporting layer that tracks price, production and supply concentration across four battery minerals: **Lithium, Graphite, Manganese and Cobalt**.

> **Capability build:** this is a RUSA Analytics demonstration built on synthetic data. It is not a client engagement, and the figures are illustrative.

## Architecture

```text
CSV sources ──► RAW schema ──► CORE star schema ──► REPORTING views ──► Power BI (DirectQuery)
               (landing zone)  (dims + fact)        (pre-aggregated)    via read-only role
```

- **RAW** mirrors the source files.
- **CORE** is a star schema: commodity, geography, supplier and date dimensions around a unified market fact table.
- **REPORTING** exposes business-ready views only. Power BI connects through a read-only service role scoped to this schema, so the semantic model never touches raw or core data.
- Measures include year-over-year price movement and a Herfindahl-Hirschman Index (HHI) for supply concentration.

## Repository files

| File | What it is |
|---|---|
| [`snowflake_setup.sql`](snowflake_setup.sql) | Warehouse, database, schema, stage, table and view build script (raw → core → reporting) |
| [`powerbi_integration_guide.md`](powerbi_integration_guide.md) | Connection method, semantic model and key DAX measures |
| [`critical_minerals_dashboard.html`](critical_minerals_dashboard.html) | Self-contained interactive dashboard (open in a browser) |
| [`CASE_STUDY.md`](CASE_STUDY.md) | Challenge, approach and outcome |
| `fact_commodity_market.csv`, `dim_commodity.csv`, `dim_geography.csv` | Synthetic source data used to build the warehouse |

## Tech stack

Snowflake (warehouse, RBAC, reporting views) · Power BI (native Snowflake connector, DirectQuery, DAX) · SQL

## About RUSA Analytics

RUSA Analytics builds business intelligence, data engineering and AI-powered analytics solutions.

- Website: [rusaanalytics.com](https://www.rusaanalytics.com)
- GitHub: [github.com/RUSA-Analytics](https://github.com/RUSA-Analytics)

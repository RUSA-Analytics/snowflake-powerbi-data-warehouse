# Case Study: Critical Minerals Market Intelligence

**Snowflake data warehouse + Power BI reporting layer**

> **Capability build:** a RUSA Analytics demonstration on synthetic data, not a named client engagement.

## At a glance

- 4 commodities tracked: Lithium, Graphite, Manganese, Cobalt
- 14 producing countries modelled across supply chains
- 3-schema warehouse (raw → core → reporting) built for least-privilege BI access

## Challenge

Procurement and strategy teams tracking battery-grade minerals typically pull price and supply data from scattered sources (exchange feeds, government trade data, individual mine disclosures) with no shared warehouse and no live reporting layer. Analysts rebuild the same spreadsheet every reporting cycle, and supply-concentration risk, where a single country or supplier dominates a mineral's production, is easy to miss without a purpose-built view.

## Approach

A three-layer Snowflake warehouse: a raw landing zone mirroring source structure, a core star schema (commodity, geography, supplier and date dimensions against a unified market fact table), and a reporting schema exposing only pre-aggregated, business-ready views.

Power BI connects via DirectQuery against those views only, through a read-only service role scoped to the reporting schema. Report measures include year-over-year price movement and a Herfindahl-Hirschman Index (HHI) on supply concentration, giving a standard, defensible risk metric rather than an ad hoc judgement.

## Outcome

- A reporting layer that reflects each new data load with no separate refresh schedule to manage.
- A security boundary enforced once, at the warehouse role, rather than duplicated in the BI tool.
- A supply-concentration view that surfaces single-country dependency risk automatically.

## Tech stack

Snowflake (warehouse, RBAC, DirectQuery-optimised views) · Power BI (native Snowflake connector, DAX) · SQL

See [`snowflake_setup.sql`](snowflake_setup.sql) and [`powerbi_integration_guide.md`](powerbi_integration_guide.md) for the build details.

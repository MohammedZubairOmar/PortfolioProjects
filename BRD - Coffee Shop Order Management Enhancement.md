# Business Requirements Document (BRD)
## Coffee Shop Order Management System Enhancement

| | |
|---|---|
| **Document Status** | Draft v0.1 |
| **Prepared By** | Mohammed Zubair Omar, Business Analyst |
| **Date** | 2026-07-29 |
| **Related Artifacts** | `coffeeOrdersRawData.xlsx`, `coffeeOrdersProject.xlsx` |

---

## 1. Executive Summary

This BRD defines the business case and requirements for enhancing the order management process at [Coffee Shop Co.], a mock mid-size coffee retailer used as the basis for this portfolio's coffee sales dataset. Analysis of historical order data (`coffeeOrdersRawData.xlsx`) surfaced recurring data-quality and reporting gaps that mirror real operational pain: orders are recorded manually or exported ad hoc, there is no single source of truth for daily sales, and management lacks a repeatable way to see performance by product, store, and time of day. This document proposes a requirements baseline for an enhanced order management and reporting capability to close those gaps.

## 2. Business Problem / Background

- Order data is captured across disconnected exports with inconsistent formatting, requiring manual cleanup before it can be analyzed (see cleaning steps applied in `coffeeOrdersProject.xlsx`).
- Store managers do not have real-time or daily visibility into sales performance, top/bottom-selling products, or peak order times.
- Leadership cannot currently answer basic questions (e.g., "which product line drives the most revenue this month?") without a manual, one-off analysis.
- There is no standard definition for key metrics (e.g., what counts as a "completed" order vs. "voided"), leading to inconsistent reporting between stores.

## 3. Business Objectives

| ID | Objective |
|----|-----------|
| OBJ-1 | Establish a single, clean, reliable source of order data for reporting |
| OBJ-2 | Give store and regional managers self-serve visibility into daily/weekly sales performance |
| OBJ-3 | Standardize key business metric definitions across all stores |
| OBJ-4 | Reduce time spent on manual data cleanup before analysis is possible |

## 4. Scope

### In Scope
- Requirements for a cleaned, standardized order data pipeline (source → clean → reporting-ready)
- Requirements for a management-facing sales dashboard (product, store, time-of-day views)
- Definition of standard metrics and business rules for order status
- Data quality rules for order records (required fields, valid ranges, deduplication)

### Out of Scope
- Point-of-sale (POS) hardware or software replacement
- Payment processing changes
- Inventory/supply chain management (may be addressed in a future phase)
- Customer loyalty program integration

## 5. Stakeholders

| Stakeholder | Role | Interest |
|---|---|---|
| Store Managers | Process Owner | Need daily visibility into store-level sales |
| Regional Operations Manager | Business Sponsor | Needs cross-store comparison and trend visibility |
| Finance | Reviewer | Needs revenue figures to reconcile with accounting records |
| Business Analyst (this role) | Requirements Owner | Gathers requirements, defines metrics, validates data quality |
| Data/Reporting Owner | Implementer | Builds the cleaning pipeline and dashboard |

## 6. Current State (As-Is) Process

1. Orders are exported from the POS system as raw spreadsheet extracts on an ad hoc basis.
2. Extracts contain inconsistent date formats, blank/null fields, and occasional duplicate order entries.
3. Analysis requires manual cleanup each time a report is requested (see transformations applied in this repo's coffee project, e.g. handling missing values, standardizing categories, removing duplicates).
4. No dashboard exists; findings are shared as static spreadsheets or ad hoc summaries.
5. Store managers have no way to self-serve — every question routes through whoever last cleaned the data.

## 7. Future State (To-Be) Process

1. Order extracts are validated and cleaned against a documented set of data quality rules immediately on receipt.
2. A standardized, cleaned dataset is maintained as the single source of truth for reporting.
3. Store and regional managers access a self-serve dashboard showing sales by product, store, and time period, updated on a defined refresh cadence.
4. Metric definitions (e.g., "net sales," "completed order") are documented once and applied consistently everywhere.
5. Ad hoc analysis requests decrease because the majority of recurring questions are answered directly in the dashboard.

## 8. Functional Requirements

| ID | Requirement | Priority |
|----|---|---|
| FR-1 | System shall standardize date/time fields to a single consistent format | Must |
| FR-2 | System shall flag or remove duplicate order records based on order ID / timestamp / amount | Must |
| FR-3 | System shall enforce required fields on each order record (order ID, product, quantity, price, store, timestamp, status) | Must |
| FR-4 | Dashboard shall display total sales by product category, filterable by date range and store | Must |
| FR-5 | Dashboard shall display sales trends by hour/day-part to support staffing decisions | Should |
| FR-6 | Dashboard shall support store-to-store comparison views | Should |
| FR-7 | System shall log and surface data quality exceptions (e.g., missing price, invalid store code) rather than silently dropping records | Must |
| FR-8 | Metric glossary shall be maintained and versioned alongside the dashboard | Could |

## 9. Non-Functional Requirements

| ID | Requirement |
|----|---|
| NFR-1 | Dashboard should load within 5 seconds for a single-store, single-month view |
| NFR-2 | Cleaned dataset must be reproducible from raw source via a documented, repeatable process (no manual one-off edits) |
| NFR-3 | Access to store-level data should be restricted to that store's management and regional/corporate roles |

## 10. Assumptions & Constraints

- **Assumption:** Raw order exports remain available in a consistent file format (spreadsheet extract) for the near term.
- **Assumption:** No changes to the POS system are required to implement this phase.
- **Constraint:** Solution should use tools already available to the business (e.g., Excel/Power BI) rather than requiring new software procurement.

## 11. Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Source data quality degrades further (e.g., new export format) | Broken pipeline, inaccurate reporting | Add validation checks that fail loudly rather than silently passing bad data |
| Store managers do not adopt the dashboard | Objective OBJ-2 not met | Involve store managers in requirements review and pilot with one store first |
| Metric definitions disputed between Finance and Operations | Delayed sign-off | Resolve definitions in a joint working session before build starts |

## 12. Success Metrics

| Metric | Target |
|---|---|
| Time to produce a standard sales report | Reduce from ~manual/ad hoc to same-day self-serve |
| Data quality exceptions in cleaned dataset | < 1% of records flagged after initial stabilization period |
| Store manager adoption of dashboard | ≥ 80% of stores actively using it monthly within 3 months of rollout |

## 13. Appendix

- **Glossary**
  - *Completed order:* An order fully paid and fulfilled, excluding voided or refunded transactions.
  - *Net sales:* Gross order value minus refunds and voided orders.
- **Related files in this repository:** `coffeeOrdersRawData.xlsx` (source), `coffeeOrdersProject.xlsx` (cleaned/analyzed output)

---
*This document is a portfolio artifact demonstrating BRD structure and business requirements analysis technique; the referenced company is illustrative, built on this repo's coffee sales dataset.*

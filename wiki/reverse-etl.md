# Reverse ETL

**Summary**: Reverse ETL is the process of syncing data directly from a central data warehouse into operational systems like CRMs, marketing automation, and customer support tools to enable data activation.
**Tags**: #data-engineering #reverse-etl #data-activation
**Created**: 2026-04-14

---

## Overview
Reverse ETL is a key component of the modern data stack that moves data from "passive" storage (where it's used for reports) to "active" use in the tools where business teams actually work. It allows every department (Marketing, Sales, Support) to operate on the same governed, consistent customer definitions from a single source of truth.

## Key Benefits
- **Data Activation**: Enables teams to take action on warehouse data within their existing workflows.
- **Single Source of Truth**: Ensures consistent data across all business tools by using the warehouse as the primary source.
- **Operational Efficiency**: Replaces manual CSV exports and fragile, custom-built API integrations.
- **Composable CDP**: Allows building a Customer Data Platform on top of an existing warehouse instead of using a siloed, external CDP.
- **Scalability & Reliability**: Batch-based processing makes it cost-effective and reliable for moving large volumes of data.

## How it Works
The process typically involves four components:
1.  **Sources**: The central data warehouse where the data lives (e.g., Snowflake, BigQuery, Redshift, Databricks).
2.  **Models**: SQL queries or dbt models that define exactly which data needs to be synced.
3.  **Destinations**: The downstream SaaS tools where the data is sent (e.g., Salesforce, HubSpot, Braze, Zendesk, Facebook Ads).
4.  **Syncs**: The configuration that defines how and when data should move (e.g., "update record if email matches").

## Reverse ETL vs. Traditional ETL
- **ETL (Extract, Transform, Load)**: Moves data **into** the warehouse for analysis and business intelligence.
- **Reverse ETL**: Moves data **out** of the warehouse into operational systems for action.

## Common Use Cases
- **Sales**: Syncing lead scores or product usage data into a CRM (like Salesforce) to prioritize outreach.
- **Marketing**: Creating dynamic audience segments in the warehouse and syncing them to ad platforms (like Facebook or Google Ads) for precise targeting.
- **Support**: Providing agents with a 360-degree view of customer history and status within support tools (like Zendesk).

## Sources
- `raw/articles/reverse-etl.md`
- `https://hightouch.com/blog/reverse-etl`

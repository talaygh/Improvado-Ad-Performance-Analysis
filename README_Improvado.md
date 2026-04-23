# Multi-Channel Ad Performance Analysis
**Take-home assignment | Snowflake · SQL · Tableau**

---

## Overview

End-to-end marketing analytics project unifying advertising data from three platforms — Facebook, Google, and TikTok — into a single data model in Snowflake, with cross-channel performance insights visualized in Tableau Public.

**Live Dashboard:** [View on Tableau Public](https://public.tableau.com/app/profile/talay.kamali/viz/Improvado/AdPerformance)

---

## Tech Stack

| Layer | Tool |
|---|---|
| Data Warehouse | Snowflake |
| Transformation | SQL (Snowflake) |
| Visualization | Tableau Public |

---

## Dataset

Three CSV files provided as part of the assignment:

- `01_facebook_ads.csv` — Facebook campaign metrics
- `02_google_ads.csv` — Google Ads campaign data
- `03_tiktok_ads.csv` — TikTok advertising engagement

All three files were uploaded to Snowflake and unified into a single table (`UNIFIED_ADS`) via `UNION ALL`, standardizing column names across platforms.

---

## SQL — Unified Table

```sql
CREATE DATABASE MARKETING_ANALYTICS;
CREATE SCHEMA MARKETING_ANALYTICS.RAW_DATA;

CREATE OR REPLACE TABLE MARKETING_ANALYTICS.RAW_DATA.UNIFIED_ADS AS

SELECT date, 'Facebook' AS platform, campaign_id, campaign_name,
       impressions, clicks, spend AS cost, conversions
FROM MARKETING_ANALYTICS.RAW_DATA.FACEBOOK_ADS

UNION ALL

SELECT date, 'Google' AS platform, campaign_id, campaign_name,
       impressions, clicks, cost, conversions
FROM MARKETING_ANALYTICS.RAW_DATA.GOOGLE_ADS

UNION ALL

SELECT date, 'TikTok' AS platform, campaign_id, campaign_name,
       impressions, clicks, cost, conversions
FROM MARKETING_ANALYTICS.RAW_DATA.TIKTOK_ADS;
```

---

## Dashboard Views

- **Cost by Platform** — Total ad spend breakdown across Facebook, Google, TikTok
- **Conversions Over Time** — Platform-level conversion trends by date
- **Click-Through Rate (CTR) by Platform** — `SUM(Clicks) / SUM(Impressions)` per platform
- **Conversions by Campaign** — Top performing campaigns ranked by conversion volume

---

## Key Insights

- Spend and conversion distribution varies significantly across platforms
- CTR differences highlight platform-level audience engagement patterns
- Campaign-level breakdown reveals which campaigns drive the most conversions relative to cost

---

## Files

| File | Description |
|---|---|
| `01_facebook_ads.csv` | Raw Facebook ads data |
| `02_google_ads.csv` | Raw Google Ads data |
| `03_tiktok_ads.csv` | Raw TikTok ads data |

---

## Author

**Talay Kamali** — Data Analyst  
[Tableau Public Profile](https://public.tableau.com/app/profile/talay.kamali/vizzes)

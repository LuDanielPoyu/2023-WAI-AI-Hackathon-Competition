# Geospatial Retail Analytics — Taiwan Breakfast Shops (WAI Data Hackathon)

**Role:** Data Scientist (Team Project)  
**When:** Nov–Dec 2023 · **Award:** 2nd place, National WAI AI Data Hackathon (industry judges, real commercial datasets)

> **Note:** This portfolio uses sanitized descriptions and **synthetic examples only**.

---

## Problem
Breakfast shop operators in Taiwan need a data-driven way to **forecast and optimize revenue** using **geospatial retail signals** (competition density, proximity to transit and schools, footfall proxies) and transaction patterns.

---

## P1 — Geospatial Site Competitiveness Scoring
**Solution:** Built a site-scoring model from **Google Maps API** open data to rank candidate locations by expected competitiveness.  
**Tech highlights:** H3/hex grid features; POI **density/proximity** metrics; distance matrix approximations; **XGBoost** with k-fold CV; **SHAP** for interpretable drivers.

---

## P2 — Customer Segmentation with K-means
**Solution:** Clustered customers to guide pricing, promotion, and assortment by segment.  
**Tech highlights:** **K-means** with **StandardScaler**, elbow/silhouette to choose *k*; **RFM**, visit time-of-day and basket composition features; post-hoc rules that map segments to **actionable plays** (e.g., commuter bundles, weekend family sets, delivery-only promos).

---

## P3 — Demand Forecasting with Prophet
**Solution:** Predicted **peak intervals** and daily revenue to inform staffing and prep.  
**Tech highlights:** **Prophet** with weekly/annual seasonality, holiday effects, and promo flags; outlier capping; interval (quantile) forecasts for risk-aware schedules.

---

## P4 — Item Popularity Ranking with Random Forest
**Solution:** Ranked menu items by expected sell-through for each site/segment.  
**Tech highlights:** **Random Forest** with price and margin, recent velocity, seasonality, and **co-purchase graph** stats; evaluated with PR-AUC and **MAP@k**; produced top-N assortments per cluster and site.

---

## P5 — Industry Scorecard for Taiwan Breakfast Shops
**Solution:** Built a concise **scorecard & report** combining site score, segment potential, and forecast quality to benchmark locations and track impact.  
**Tech highlights:** Weighted composite index (simple AHP/normalized z-scores); small **BI dashboard** for “where to open / what to stock / when to staff”; exportable playbook.

---

## Stack
**Python**, **pandas**, **scikit-learn**, **XGBoost**, **Prophet**, **SHAP**, **NetworkX** (co-purchase graphs), **H3** (spatial grids), **Google Maps POI features**


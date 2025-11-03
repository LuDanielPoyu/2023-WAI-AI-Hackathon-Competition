# Geospatial Retail Analytics — Taiwan Breakfast Shops (WAI Data Hackathon)

**Role:** Data Scientist (Team Project)  
**When:** Nov–Dec 2023 · **Award:** 2nd place, National WAI AI Data Hackathon (industry judges, real commercial datasets)

> **Note:** This portfolio uses sanitized descriptions and **synthetic examples only**.  
> No proprietary data, partner IDs, or credentials are included.

---

## Problem: 
Breakfast shop operators in Taiwan need a data-driven way to **forecast and optimize revenue** using **geospatial signals** (competition density, public transit proximity, neighborhood income) and transaction patterns.

---

## P1 — Geospatial Site Competitiveness Scoring
**Solution:** Scored candidate locations by expected profitability using geospatial features and composite index.

**Highlights:**
- **Features:** population density, bus-stop density, neighborhood median income, breakfast-shop density (Google Maps POI).
- **Revenue class model:** **Random Forest** classifier to predict expected revenue tier; accuracy ~0.65 on holdout; dropping “bus density” improved accuracy.
- **Cost proxy:** expected rent (area rental) standardized by locality.
- **Score:** **standardized expected revenue – standardized expected rent**, then mapped to a **0–5 competitiveness score** for easy ranking.

---

## P2 — Customer Segmentation (K-means)
**Solution:** Clustered customers to guide pricing, promotions, delivery radius, and bundles.

**Highlights:**
- **Features:** order timestamp, **net amount**, party size, **service type** (takeout / dine-in / delivery), **platform** (Foodpanda / iChef / instore / UberEats), **order type**.
- **Method:** **K-means** with scaling; silhouette/elbow to pick *k*.  
- **Segments:** (1) **High-value delivery**, (2) **Habitual takeout**, (3) **Dine-in experience**.
- **Plays:** LINE preorder for takeout, delivery within a set radius for delivery segment, **group-order discounts** for nearby offices, **hotel breakfast partnership** where present.

---

## P3 — Demand Forecasting & Peak-Hour Windows (Prophet)
**Solution:** Forecasted daily revenue and **best time intervals to serve customers** for staffing and prep.

**Highlights:**
- **Model:** **Prophet** with weekly/annual seasonality, **holiday effects**, school-break flags, **COVID indoor-dining ban** period, and **custom business-hours seasonality**.  
- **Validation:** backtesting by store; typical **R² ~0.4–0.7** depending on data quality.

---

## P4 — Item Popularity Ranking (Random Forest)
**Solution:** Predicted **per-day item ranks** to shape assortment and promos.

**Highlights:**
- **Targets & inputs:** predict item rank for **2023-10-07 → 2023-10-13** from historical sales; key fields include **product name** (one-hot), **invoice date/time**, and derived velocity features.  
- **Model:** **Random Forest**; produced **top-N lists** per store/date and a **rank lookup** (get a specific item’s rank or the top-N on a day).

---

## P5 — Industry Scorecard for Taiwan Breakfast Shops
**Solution:** A concise **scorecard** combining **site score**, **segment potential**, and **forecast quality** to benchmark locations and track impact; delivered as a small BI view and exportable report.

---

## Results (summary)
- Clear, interpretable **site competitiveness score (0–5)** derived from revenue vs. rent signals. 
- **Actionable segment playbook** (preorder, delivery radius, group discounts, hotel partnership). 
- **Prophet** forecasts identify **peak intervals** and daily revenue; **R² ~0.4–0.7** by store. 
- **Random Forest** item ranking with date-specific top-N outputs and rank lookup utilities. 

---

## Stack
**Python**, **pandas**, **scikit-learn**, **XGBoost/RandomForest**, **Prophet**, **SHAP**, **Google Maps POI features**

---

## Quick Start (synthetic demo)
```bash
pip install -r requirements.txt
# 1) Customer segments
jupyter nbconvert --to notebook --execute notebooks/02_customer-segmentation-kmeans.ipynb
# 2) Peak-interval & revenue forecast
jupyter nbconvert --to notebook --execute notebooks/03_demand-forecast-prophet.ipynb
# 3) Item ranking
jupyter nbconvert --to notebook --execute notebooks/04_item-ranking-random-forest.ipynb

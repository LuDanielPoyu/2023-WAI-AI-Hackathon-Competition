# Geospatial Retail Analytics — Taiwan Breakfast Shops (WAI Data Hackathon)

**Role:** Data Scientist (Team Project)  

**When:** Nov–Dec 2023  

**Award:** 2nd place, National WAI AI Data Hackathon (industry judges, real commercial datasets)

> **Note:** This portfolio uses sanitized descriptions and **synthetic examples only**.  
> No proprietary data, partner IDs, or credentials are included.

---

## Problem
Breakfast shop operators in Taiwan need a data-driven way to **forecast and optimize revenue** using **geospatial signals** (competition density, public transit proximity, neighborhood income) and transaction patterns.

---

## P1 — Geospatial Site Competitiveness Scoring
**Solution:** Scored candidate locations by expected profitability using geospatial features and a composite index.

**Highlights:**
- **Features:** Population density, bus stop density, neighborhood median income, breakfast-shop density (Google Maps Places POI).
- **Revenue class model:** **Random Forest** classifier to predict expected revenue tier; accuracy ~0.65 on a hold-out set; dropping “bus density” improved accuracy.
- **Cost proxy:** Expected rent (area asking rent) standardized by locality.
- **Score:** **Standardized expected revenue − standardized expected rent**, then mapped to a **0–5 competitiveness score** for easy ranking.
  
<img width="567" height="600" alt="site-score-map" src="https://github.com/user-attachments/assets/d2c4c29a-5765-4999-a83c-cee417e65ed6" />
<img width="567" height="487" alt="site-score-hist" src="https://github.com/user-attachments/assets/e0114a91-a4f2-4ad6-af4f-394aba3ae785" />

---

## P2 — Customer Segmentation (K-means)
**Solution:** Clustered customers to guide pricing, promotions, delivery radius, and bundles.

**Highlights:**
- **Features:** Order timestamp, **net amount**, party size, **service type** (takeout / dine-in / delivery), **platform** (Foodpanda / iChef / in-store / UberEats), **order type**.
- **Method:** **K-means** with feature scaling; silhouette and elbow methods to pick *k*.  
- **Segments:** (1) **High-value delivery**, (2) **Habitual takeout**, (3) **Dine-in experience**.
- **Plays:** LINE pre-order for takeout, delivery within a set radius for the delivery segment, **group-order discounts** for nearby offices, and **hotel breakfast partnerships** where present.
  
<img width="567" height="487" alt="kmeans-clusters" src="https://github.com/user-attachments/assets/0064ba86-7d99-4d92-945d-b20dab95dadd" />

---

## P3 — Demand Forecasting & Peak-Hour Windows (Prophet)
**Solution:** Forecasted daily revenue and **best time intervals to serve customers** for staffing and prep.

**Highlights:**
- **Model:** **Prophet** with weekly/annual seasonality, **holiday effects**, school-break flags, **COVID indoor-dining ban** period, and **custom business-hours seasonality**.  
- **Validation:** Back-testing by store; typical **R² ~0.4–0.7** depending on data quality.

<img width="567" height="487" alt="prophet-forecast" src="https://github.com/user-attachments/assets/1a7f41e3-d48b-4906-9c57-42ce3bd35ac7" />

---

## P4 — Item Popularity Ranking (Random Forest)
**Solution:** Predicted **per-day item ranks** to shape assortment and promos.

**Highlights:**
- **Targets & inputs:** Predicted item rank for **2023-10-07 → 2023-10-13** from historical sales; key fields include **product name** (one-hot), **invoice date/time**, and derived velocity features.  
- **Model:** **Random Forest**; produced **top-N lists** per store/date and a **rank lookup** (get a specific item’s rank or the top-N on a day).
 
<img width="567" height="487" alt="item-ranking" src="https://github.com/user-attachments/assets/9cdf8e8a-6112-4117-97a4-31b1bafab127" />

---

## P5 — Industry Scorecard for Taiwan Breakfast Shops
**Solution:** A concise **scorecard** combining **site score**, **segment potential**, and **forecast quality** to benchmark locations and track impact; delivered as a small BI view and exportable report.

<img width="567" height="487" alt="industry-scorecard" src="https://github.com/user-attachments/assets/98fd78af-f252-4323-948f-57282fb10485" />

---

## Results (summary)
- Clear, interpretable **site competitiveness score (0–5)** derived from revenue vs. rent signals. 
- **Actionable segment playbook** (pre-order, delivery radius, group discounts, hotel partnerships). 
- **Prophet** forecasts identify **peak intervals** and daily revenue; **R² ~0.4–0.7** by store. 
- **Random Forest** item ranking with date-specific top-N outputs and rank lookup utilities. 

---

## Stack
**Python**, **pandas**, **scikit-learn**, **Random Forest**, **Prophet**, **SHAP**, **Google Maps Places features**
<!-- If you also used XGBoost, keep it here; otherwise remove it for consistency. -->

---

## Quick Start (synthetic demo)
```bash
pip install -r requirements.txt

# 1) Competitiveness scores
jupyter nbconvert --to notebook --execute notebooks/01_site-competitiveness-score_random-forest.ipynb

# 2) Customer segments
jupyter nbconvert --to notebook --execute notebooks/02_customer-segmentation-kmeans.ipynb

# 3) Peak-interval & revenue forecast
jupyter nbconvert --to notebook --execute notebooks/03_demand-forecast-prophet.ipynb

# 4) Item ranking
jupyter nbconvert --to notebook --execute notebooks/04_item-ranking-random-forest.ipynb

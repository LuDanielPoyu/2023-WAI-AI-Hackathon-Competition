# Geospatial Retail Site Selection & Demand Forecasting — WAI Data Hackathon

**Role:** Data Scientist 
**When:** Nov 2023 – Dec 2023 · **Award:** 2nd place, National WAI AI Data Hackathon (industry judges, commercial datasets)

> **Disclaimer:** This portfolio uses sanitized descriptions and **synthetic examples only**.  
> No proprietary data, partner IDs, or credentials are included.

---

## Problem
A retailer needed to **rank candidate store locations** and **forecast demand**. Existing heuristics ignored local competition density and time-of-day patterns, leading to sub-optimal site picks and staffing.

---

## P1 — Geospatial Site Competitiveness Scoring
**Solution:** Built an **XGBoost** model to score each candidate site using **point-of-interest (POI) density and proximity features** gathered from Google Maps.

**Highlights**
- **Data:** Aggregated POIs by category and radius; computed counts, distances, nearest-neighbor stats, and simple travel-time proxies.  
- **Features:** Density and proximity signals (competitors, complementary stores, transit), catchment summaries, and grid smoothing to reduce sparsity.  
- **Training:** XGBoost with k-fold cross-validation; early stopping and basic hyperparameter search.  
- **Explainability:** **SHAP** to visualize top drivers and compare “good vs. weak” sites.  
- **Output:** Ranked list of sites with score, key drivers, and quick notes for business review.

**Impact**
- **Competition result:** **2nd place overall**; clear, interpretable drivers helped justify recommendations to judges.

**Pipeline (simplified)**
```mermaid
flowchart LR
  A[Candidate sites] --> B[Gather POIs]
  B --> C[Engineer density and proximity features]
  C --> D[Train XGBoost with k fold]
  D --> E[SHAP explanations]
  E --> F[Ranked site list]

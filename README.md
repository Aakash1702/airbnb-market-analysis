# Airbnb Market Analysis: Guest Behavior & Economic Impact

An end-to-end data analysis project examining how guest demographics, travel behavior, and listing characteristics drive booking performance and local economic impact across 7 US markets - using SQL, Python, and causal inference methods.

---

## Background

This project applies a **Destination Management Organization (DMO) lens** to Airbnb platform data. Having worked in visitor analytics at Destination Cleveland - studying how travelers perceive cities and how their spending influences local economic growth - I wanted to explore the same questions from the platform side.

The core question: *how does visitor behavior on Airbnb translate into real economic outcomes for cities?*

---

## Tools & Technologies

| Layer | Tools |
|---|---|
| Data generation | Python · Faker · NumPy |
| Storage | SQL Server 2014 · Databricks (Unity Catalog) |
| Querying | T-SQL · Spark SQL |
| Analysis & visualization | Python · Pandas · Matplotlib · Seaborn · Statsmodels |
| Environment | Databricks (Serverless Warehouse) |

---

## Dataset

Synthetic dataset designed to reflect realistic Airbnb market dynamics across 7 US cities.

| Table | Rows | Description |
|---|---|---|
| `guests` | 10,000 | Demographics, travel purpose, booking history |
| `hosts` | 1,200 | Superhost status, response rates, ratings |
| `listings` | 2,093 | Room type, pricing, amenities, neighborhood |
| `bookings` | 10,000 | Check-in/out, party size, status, fees |
| `spending` | 32,558 | 8 spend categories per completed stay |

**Cities covered:** New York City · Los Angeles · Chicago · Miami · Nashville · Austin · Portland

---

## Project Structure

```
airbnb-market-analysis/
│
├── airbnb_analysis.ipynb            # Phase 1 + 2: SQL queries + visualizations
├── airbnb_causal_inference.ipynb    # Phase 3: Causal inference analysis
├── generate_dataset.py              # Synthetic data generation script
└── README.md                        # This file
```

---

## Phase 1 + 2: Descriptive Analysis & Visualization

### Key Findings

**1. Miami is a high-yield market, NYC is a high-volume market**
Miami leads total revenue ($1.27M) despite ranking 4th in bookings - driven by a $1,040 avg booking value vs NYC's $753. These markets require fundamentally different growth strategies.

**2. Cancellation rates are platform-driven, not market-driven**
All 7 cities cluster tightly between 16-19%. The near-uniform distribution suggests platform-level policies dominate over local market factors.

**3. Business and Events travelers punch above their weight**
Business + Events travelers represent ~20% of stays but generate ~28% of total spending - consistent with DMO research on high-yield visitor segments.

**4. Shopping & Retail is the top per-night spend category in premium markets**
NYC and Miami visitors spend $443 and $438 per night on retail - outpacing dining in high-cost markets.

**5. Superhost status commands a 10.5% raw booking value premium**
Superhosts earn $834 avg per booking vs $755 for regular hosts. See Phase 3 for the causal analysis of this finding.

---

## Phase 3: Causal Inference

Moving beyond "what happened" to "why" - using OLS regression and logistic regression to isolate true causal effects from confounded correlations.

### Question 1 - Does superhost status cause higher revenue?

| | Value |
|---|---|
| Raw premium (Phase 2) | $79.04 |
| After controlling for listing quality, city, room type | $16.50 |
| Explained by confounders | $62.55 (79%) |
| P-value | 0.23 - not significant |

**Finding:** The superhost badge itself does not cause higher revenue. 79% of the raw premium is explained by underlying listing quality - better properties in premium cities with more bedrooms. Airbnb's superhost program rewards quality more than it creates it.

---

### Question 2 - Does booking lead time cause lower cancellation?

| | Value |
|---|---|
| Raw: 0-7 day cancellation rate | 17.2% |
| Raw: 8-30 day cancellation rate | 15.4% |
| Odds ratio after controls | 1.0009 |
| P-value | 0.12 - not significant |

**Finding:** Lead time has no causal effect on cancellation after controlling for guest and listing characteristics. Last-minute bookers cancel slightly more in raw data, but the effect disappears entirely once you account for who they are and what they're booking.

---

### Question 3 - Does longer stay cause more local economic impact?

| | Value |
|---|---|
| Raw correlation (Pearson r) | 0.89 |
| Causal effect per extra night | $1,968 |
| 95% Confidence interval | ($1,946 - $1,990) |
| P-value | < 0.0001 - highly significant |
| R-squared | 0.81 |

**Finding:** Stay duration has a genuine, significant causal relationship with local economic impact - confirmed after controlling for city, travel purpose, age group, and party size. Every extra night generates ~$1,968 in additional local spending.

**DMO implication:** Policies that extend average stay length by just 1 night across 7,000 completed bookings would generate ~$13.8M in additional local economic impact.

---

## Causal Inference Summary

| Question | Raw finding | After controls | Verdict |
|---|---|---|---|
| Superhost premium | $79 higher revenue | $16 - p=0.23 | Listing quality drives it, not the badge |
| Lead time & cancellation | 0-7 days cancels most | Odds ratio ~1.0 - p=0.12 | Guest profile drives it, not timing |
| Stay duration & spending | r=0.89 correlation | $1,968/night - p<0.0001 | Genuine causal effect confirmed |

---

## How to Run

### In Databricks
1. Upload `airbnb_synthetic_dataset.xlsx` to a Unity Catalog Volume
2. Import both `.ipynb` notebooks into your Databricks workspace
3. Connect to a Serverless Warehouse and run all cells

### Locally (VS Code / Jupyter)
Replace `spark.sql(...).toPandas()` calls with `pd.read_excel()` reading from the local Excel file.

---

## About

Built as part of a data analytics portfolio to demonstrate proficiency in SQL, Python, Spark, Databricks, and causal inference - with a focus on travel and economic impact analytics.

**Background:** Research at Destination Cleveland, with experience in visitor analytics and insights reporting.

**Connect:** [LinkedIn](https://linkedin.com) | [GitHub](https://github.com)

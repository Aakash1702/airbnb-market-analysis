# Airbnb Market Analysis: Guest Behavior & Economic Impact

A end-to-end data analysis project examining how guest demographics, travel behavior, and listing characteristics drive booking performance and local economic impact across 7 US markets.

---

## Background

This project applies a **Destination Management Organization (DMO) lens** to Airbnb platform data. Having worked in visitor analytics at Destination Cleveland — studying how travelers perceive cities and how their spending influences local economic growth — I wanted to explore the same questions from the platform side.

The core question: *how does visitor behavior on Airbnb translate into real economic outcomes for cities?*

---

## Tools & Technologies

| Layer | Tools |
|---|---|
| Data generation | Python · Faker · NumPy |
| Storage | SQL Server 2014 · Databricks (Unity Catalog) |
| Querying | T-SQL · Spark SQL |
| Analysis & visualization | Python · Pandas · Matplotlib · Seaborn |
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

## Key Findings

### 1. Miami is a high-yield market, NYC is a high-volume market
Miami leads total revenue ($1.27M) despite ranking 4th in bookings — driven by a $1,040 avg booking value vs NYC's $753. These markets require fundamentally different growth strategies.

### 2. Cancellation rates are platform-driven, not market-driven
All 7 cities cluster tightly between 16–19% cancellation rate. The near-uniform distribution suggests platform-level policies dominate over local market factors.

### 3. Business and Events travelers punch above their weight
Business + Events travelers represent ~20% of stays but generate ~28% of total spending — a disproportionate economic impact consistent with DMO research on high-yield visitor segments.

### 4. Shopping & Retail is the top per-night spend category in premium markets
NYC and Miami visitors spend $443 and $438 per night on retail alone — outpacing dining in high-cost markets. Dining dominates in mid-tier cities like Austin and Portland.

### 5. Superhost status commands a 10.5% booking value premium
Superhosts earn $834 avg per booking vs $755 for regular hosts — a $79 premium on just a $7.70 higher nightly rate. Trust and quality signals amplify revenue beyond price alone.

---

## Project Structure

```
airbnb-market-analysis/
│
├── airbnb_analysis.ipynb       # Main notebook — SQL queries + visualizations
├── generate_dataset.py         # Synthetic data generation script
├── README.md                   # This file
```

---

## How to Run

### In Databricks
1. Upload `airbnb_synthetic_dataset.xlsx` to a Unity Catalog Volume
2. Run `generate_dataset.py` or load the Excel file using the data loading notebook
3. Import `airbnb_analysis.ipynb` into your Databricks workspace
4. Connect to a Serverless Warehouse and run all cells

### Locally (VS Code / Jupyter)
Replace `spark.sql(...).toPandas()` calls with `pd.read_excel()` reading from the local Excel file. All visualization code runs without modification.

---

## Visualizations

| Chart | Type | Key Insight |
|---|---|---|
| Revenue by city | Horizontal bar | Miami leads on yield, NYC on volume |
| Cancellation rate | Bar + threshold line | Uniform ~18% across all markets |
| Travel purpose spend vs volume | Bubble scatter | Events/Business = high yield, low volume |
| Spend per night heatmap | Seaborn heatmap | Shopping dominates NYC/Miami |
| Superhost premium | Grouped bar | 10.5% booking value premium |

---

## Next Steps — Phase 3: Causal Inference

- Does superhost status *cause* higher revenue, or do better hosts self-select?
- Does longer booking lead time *cause* lower cancellation rates?
- Does longer stay duration *cause* higher local economic impact?

*Planned tools: statsmodels · OLS regression · difference-in-differences*

---

## About

Built as part of a data analytics portfolio to demonstrate proficiency in SQL, Python, Spark, and Databricks — with a focus on travel and economic impact analytics.

**Background:** Research Associate at Destination Cleveland, with experience in visitor analytics, economic impact modeling, and insights reporting.

**Connect:** [LinkedIn](https://linkedin.com) | [GitHub](https://github.com)

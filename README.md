# Product Portfolio & Margin Intelligence Dashboard

An interactive R Shiny dashboard for analyzing SKU-level profitability, identifying margin erosion, and surfacing pricing optimization opportunities across a product portfolio.

Built as a portfolio project to demonstrate applied pricing analytics using real retail transaction data.

---
## Links

dashboard:https://joshwtacker.shinyapps.io/margin_dashboard/

Google Slides: https://docs.google.com/presentation/d/1AjdF5stCDK_Uky2T5YnsoLyn6UqBrDyx98XEkBvRw-s/edit?slide=id.p1#slide=id.p1

---

## The Problem

Most product portfolios have the same issues hiding in plain sight:

- A significant chunk of SKUs are actively losing money
- Tail-end products consume operational bandwidth while contributing almost nothing to revenue
- Discounting practices erode margin in ways that aren't always visible until it's too late
- No single view connects pricing decisions to margin outcomes across the full portfolio

This dashboard gives pricing and product managers the visibility to act on all four.

---

## What It Found

Working with 51,290 transactions across 10,768 unique SKUs from 2011–2014:

- **28% of SKUs have negative margin** — over 3,000 products losing money on every sale
- **2,154 tail-end SKUs generate only 1.1% of total revenue** — a massive complexity cost for minimal return
- **Discounts above 30% always produce negative margin** — across every category, every time
- **Tables sub-category averages -8.5% margin** vs Paper at +24.2% — a 32-point spread within the same company
- **Average portfolio margin is only 7.7%** — with enormous room for improvement through mix shift alone

---

## Dashboard Structure

The app is organized into five analytical views, all connected to shared global filters (Category, Segment, Year).

**Portfolio Overview**
The Monday morning view. Six KPI cards show revenue, profit, margin %, negative margin SKU count, tail-end SKU count, and total SKUs at a glance. Supported by a revenue/profit breakdown by sub-category, a category revenue mix pie chart, and a monthly trend line that makes seasonality immediately visible.

**Margin Management**
Three alert cards at the top surface the most urgent issues: which SKUs are losing money, the scope of tail-end complexity, and the single best mix-shift opportunity. Below that, a margin-by-sub-category horizontal bar chart uses red/orange/green color coding to make the problem obvious without requiring any analysis. A discount impact chart and margin distribution histogram round out the tab.

**Price Optimization**
The centerpiece is a price vs. margin scatter plot where every bubble is a SKU, sized by revenue. Hovering reveals the product name, margin, and revenue. This is how you find products that are priced wrong — either underpriced high-margin SKUs or overpriced low-margin ones. Supported by a discount band analysis and a sub-category opportunity matrix.

**Channel & Region**
Breaks margin down by customer segment (Consumer, Corporate, Home Office), region, ship mode, and country. The region bubble chart plots revenue against margin — high-revenue, low-margin regions are the biggest pricing opportunity.

**SKU Explorer**
An operational tool. Filter the full 10,768-SKU table to show all SKUs, negative-margin only, tail-end only, or high-margin (>20%) products. Margin column is color-coded: red below 0%, orange between 0-10%, green above 10%. Sortable by any column.

---

## Tech Stack

| Layer | Tool |
|-------|------|
| Data processing | Python (Pandas, NumPy) |
| Storage | CSV flat files |
| Dashboard | R Shiny + shinydashboard |
| Charts | Plotly |
| Tables | DT (DataTables) |

---

## Data

**Source:** Global Superstore Dataset (Kaggle)
**Coverage:** 2011–2014, global retail transactions
**Size:** 51,290 rows, 10,768 unique SKUs
**Categories:** Technology, Furniture, Office Supplies

**Derived fields:**
- `Cost = Sales - Profit`
- `Margin_Pct = Profit / Sales * 100`
- `Discount_Band` — bucketed into 7 ranges from 0% to >50%
- `Is_Tail` — bottom 20% of SKUs by revenue

**Processed datasets saved for the dashboard:**
- `transactions.csv` — cleaned transaction-level data
- `sku_summary.csv` — aggregated stats per SKU
- `category_summary.csv` — margin and revenue by sub-category
- `region_summary.csv` — performance by region, country, and segment
- `monthly_trend.csv` — revenue and profit over time
- `discount_impact.csv` — margin outcomes by discount band

---

## Running Locally

**Prerequisites:** R, RStudio, Python 3, the following R packages:

```r
install.packages(c("shiny", "shinydashboard", "dplyr", 
                   "plotly", "DT", "scales", "tidyr"))
```

**Setup:**

1. Download the Global Superstore dataset from Kaggle and place it at `data/Global_Superstore2.csv`
2. Run the data preparation notebook to generate the processed CSVs:
```bash
jupyter notebook notebooks/data_wrangling.ipynb
```
3. Open `app.R` in RStudio and click Run App

---

## Project Structure

```
margin_dashboard/
├── app.R                          # Shiny dashboard
├── data/
│   ├── Global_Superstore2.csv     # Raw data (download from Kaggle)
│   └── processed/
│       ├── transactions.csv
│       ├── sku_summary.csv
│       ├── category_summary.csv
│       ├── region_summary.csv
│       ├── monthly_trend.csv
│       └── discount_impact.csv
└── notebooks/
    └── data_wrangling.ipynb       # Data prep and EDA
```

---

## Skills Demonstrated

- Translating a business problem (pricing managers lack visibility) into an analytical product
- SKU-level profitability analysis and portfolio segmentation
- Price/volume/mix thinking applied to real transaction data
- Building interactive dashboards with reactive filtering in R Shiny
- Communicating findings through design choices (color coding, alert cards, KPI layout) rather than just charts

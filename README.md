# 🍽️ Restaurant Chain Performance Analytics
### End-to-End Data Engineering & Business Intelligence Pipeline

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Apache Spark](https://img.shields.io/badge/Apache%20Spark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![SQL](https://img.shields.io/badge/SQL-4479A1?style=for-the-badge&logo=postgresql&logoColor=white)

---

## 📌 Project Overview

A full-scale data engineering and business intelligence project analyzing **11.1 million restaurant transactions** across a multi-branch Egyptian restaurant chain. Raw data (~1.5 GB across 9 files) was uploaded to **Databricks**, merged and transformed using **Spark SQL**, then connected live to a **4-page interactive Power BI dashboard** — uncovering critical insights around revenue patterns, branch performance, product mix, customer satisfaction, and profitability.

| Metric | Value |
|--------|-------|
| Total Revenue | EGP 2.90 Billion |
| Total Orders | 11.1 Million |
| Total Customers | 200K |
| Average Order Value | EGP 260.87 |
| Profit Margin | 94.63% |
| Branches | 6 |
| Categories | 5 |
| Menu Items | 15 |
| Total Quantity Sold | 35.6 Million |

---

## 🗂️ Repository Structure

```
restaurant-analytics/
│
├── data/                        # Source data (not tracked — see note below)
│   ├── orders.csv
│   ├── customers.csv
│   ├── branches.csv
│   ├── products.csv
│   ├── categories.csv
│   ├── payments.csv
│   ├── order_items.csv
│   ├── ratings.json
│   └── promotions.json
│
├── powerbi/
│   └── restaurant_dashboard.pbix
│
├── screenshots/
│   ├── Overview Page.png
│   ├── Orders Page.png
│   ├── Products Page.png
│   └── Other Details.png
│
└── README.md
```

> ⚠️ **Note:** Raw data files (~1.5 GB) are not tracked due to size. Use `.gitignore` or Git LFS for large file management.

---

## 🏗️ Architecture & Pipeline

```
Raw Data (1.5 GB)          Databricks                  Power BI
──────────────────    ────────────────────────    ──────────────────────
7 CSV Files        →  Upload to DBFS           →  4-Page Interactive
2 JSON Files          Spark SQL Merge &            Dashboard (Live)
                      Transformation
                      (Delta Lake)
```

### Data Flow Steps

1. **Ingestion** — Uploaded all 9 source files to Databricks File System (DBFS)
2. **Parsing** — Read CSVs with automatic schema inference; parsed nested JSON files
3. **Merging** — Unified all tables via Spark SQL JOINs into a single master analytical table (~11M rows)
4. **Enrichment** — Computed derived fields: profit margin %, weekend/weekday flag, order type labels, hourly aggregations
5. **Connection** — Linked Power BI directly to Databricks via Partner Connect for a live data connection

---

## 📦 Data Sources

| File | Type | Description |
|------|------|-------------|
| `orders.csv` | CSV | Core transaction records |
| `customers.csv` | CSV | Customer demographics & IDs |
| `branches.csv` | CSV | Branch location metadata |
| `products.csv` | CSV | Menu item details & pricing |
| `categories.csv` | CSV | Product category hierarchy |
| `payments.csv` | CSV | Payment method per order |
| `order_items.csv` | CSV | Line-item breakdown per order |
| `ratings.json` | JSON | Customer satisfaction scores |
| `promotions.json` | JSON | Discount & promotion records |

**Total Size:** ~1.5 GB | **Total Rows:** ~11 million

---

## 📊 Power BI Dashboard

The dashboard spans **4 pages**, each with shared cross-filter slicers for: **Year, Month, Day, Branch, Category, and Payment Method.**

---

### Page 1 — Overview

![Overview Page](Overview%20Page.png)

**KPIs:** Total Revenue (EGP 2.90B) · Average Order Value (EGP 260.87) · Profit Margin (94.63%) · Average Price (EGP 86) · Revenue per Customer (EGP 14.49K)

**Visuals:**
- 📈 Line chart: Total revenue by date (2020–2025) — shows flat growth trajectory
- 📊 Bar chart: Revenue by individual menu item ranked — Kebab leads at ~EGP 510M
- 🟩 Treemap: Revenue by category — Grills (EGP 1.01B) · Tagines (EGP 0.81B) · Starters (EGP 0.34B) · Poultry (EGP 0.54B) · Beverages (EGP 0.20B)
- 📊 Bar chart: Revenue by branch — Cairo clearly dominates, Assiut is the lowest
- 🍩 Donut: Revenue by payment method — Cash 50% (EGP 1.45B) · Card 30% (EGP 0.87B) · Wallet 20% (EGP 0.58B)

---

### Page 2 — Orders

![Orders Page](Orders%20Page.png)

**KPIs:** Total Orders (11.1M) · Total Customers (200K) · Average Discount (3.6%) · Revenue per Customer (EGP 14.49K) · Total Revenue (EGP 2.90B)

**Visuals:**
- 📈 Line chart: Orders by hour — dual peaks at 13:00–16:00 and 19:00–23:00
- 📈 Line chart: Average order value by month — peaks around month 9–10
- 📊 Bar chart: Rating distribution per order count — 4-star is dominant, 5-star is underrepresented
- 🍩 Donut: Revenue by order type — Dine-in 39.98% (EGP 1.16B) · Takeaway 30.03% (EGP 0.87B) · Delivery 29.99% (EGP 0.87B)

---

### Page 3 — Products

![Products Page](Products%20Page.png)

**KPIs:** Total Items (15) · Total Quantity Sold (35.6M) · Branches (6) · Categories (5) · Total Revenue (EGP 2.90B)

**Visuals:**
- 📊 Bar chart: Items growing vs. declining over time (slope coefficients) — Stuffed Eggplant declining fastest at -1.33
- 📊 Bar chart: Items by quantity sold — Mango Juice leads at 4.3M units; bottom items at 0.7M
- 📊 Bar chart: Top 5 products by revenue — Kebab · Chicken Tagine · Kofta · Molokhia Tagine · Bamia Tagine
- 📊 Bar chart: Bottom 5 products — Tea (EGP 20M) · Rural Juice · Rural Salad · Cane Juice · Stuffed Eggplant (EGP 61–108M)

---

### Page 4 — Other Details

![Other Details Page](Other%20Details.png)

**KPIs:** Total Revenue (EGP 2.90B) · Average Order Value (EGP 260.87) · Total Orders (11.1M) · Average Price (EGP 86) · Total Quantity (35.6M)

**Visuals:**
- 🕹️ Gauge: Chain-wide average rating — **3.70 / 5.0**
- 🍩 Donut: Weekend vs. weekday revenue split — Weekend 50.03% · Weekday 49.97%
- 📋 Table: Peak hours by branch — Cairo dominates every top slot (hours 20, 22, 13, 21, 16, 23, 14, 15)
- 📈 Line chart: Profit margin % by day of week — Weekends spike to ~95.5%, weekdays drop to ~93.5%

---

## 📈 Key Findings & Strategic Analysis

### Executive Summary

The restaurant chain demonstrates stable operational performance with EGP 2.90B in revenue, but reveals critical strategic opportunities in customer engagement, branch optimization, and profit margin enhancement. The data uncovers a **3.5x performance gap** between the best and worst branches, a **92% profit margin differential** between weekends and weekdays, and significant untapped cross-selling potential.

---

### 1. Revenue Patterns & Growth Dynamics — Flat Growth Signals Market Saturation

Year-over-year revenue shows minimal growth ranging from **-3.4% to +2.0%**, indicating market maturity and potential saturation in current locations. Average order value remains stable at approximately **EGP 260**, meaning growth must come from customer acquisition or visit frequency — not from pricing alone.

**Business Interpretation:**
- Stagnant growth suggests the chain has captured most available market share in existing locations
- February consistently underperforms due to fewer calendar days, but the -3.4% YoY decline in Feb 2021 indicates deeper issues beyond seasonality
- Geographic expansion is now critical — existing markets show clear signs of saturation
- Customer retention programs are essential since organic growth can no longer be relied upon
- Product innovation is needed to drive repeat frequency among existing customers

---

### 2. Branch Performance — The Cairo Advantage

Cairo dramatically outperforms all other branches with **8.93 orders per customer** compared to just **2.58 in Assiut** — a 246% difference. This translates to Cairo generating **EGP 5,071 per customer** versus only **EGP 773 in Assiut**.

| Branch | Orders/Customer | Revenue/Customer | Avg Rating | Dine-in % |
|--------|----------------|-----------------|-----------|-----------|
| Cairo | 8.93 | EGP 5,071 | 4.0 | 60.4% |
| Alexandria | — | — | 3.8 | — |
| Assiut | 2.58 | EGP 773 | 3.1 | 43.4% |

**Why Cairo Dominates:**
- Location density gives Cairo better foot traffic and accessibility
- 60.4% dine-in rate vs. 43.4% in Assiut — Cairo's ambiance and experience drive repeat visits
- Cairo attracts higher-frequency customers such as office workers and repeat diners
- Higher ratings (4.0 vs. 3.1) are the primary driver of repeat visits — every 0.1 rating point increase equals approximately 0.7 additional orders per customer

**The Assiut Problem:**
- Only 2.58 orders per customer — customers visit once and do not return
- Lowest revenue per customer (EGP 773) signals critically poor customer lifetime value
- 3.1 average rating (lowest in the chain) is the root cause — dissatisfied customers do not come back
- 43% dine-in rate suggests the restaurant experience is not compelling enough to drive repeat occasions

**Strategic Actions:**
1. Immediate operational audit in Assiut — retrain staff, upgrade facilities, review management
2. Replicate Cairo's success across other branches — study menu mix, service standards, and physical layout
3. Consider closing or relocating Assiut if no measurable improvement within 6 months
4. Expand in Cairo — with 8.93 orders per customer, there is proven demand for additional locations

---

### 3. Profit Margin Crisis — The Weekend-Weekday Gap

Weekends generate **~95.5% profit margins** compared to **~93.5% on weekdays** — a 92% margin differential. This is driven by 33% higher average order values on weekends (EGP 305 vs. EGP 229) and 92% higher discount rates applied on weekdays despite weekdays already having a lower-margin item mix.

**The Root Cause:**
- Weekday customers receive disproportionately higher discounts (2.59% avg) — but this is backwards; weekday volume should be protected through margin, not eroded through discounts
- Weekday customers tend to order quick lunches (lower-margin items) while weekend customers order premium family meals and grills
- Weekday order volume is 11% higher (2.15M vs. 1.94M orders), so even small margin improvements have massive chain-wide impact

**Financial Impact:**
- An estimated **EGP 34.5M is left on the table annually** by not optimizing weekday margins (2.39% margin gap × EGP 1.45B weekday revenue)

**Strategic Actions:**
1. Reverse the discount strategy — reduce weekday discounts by 50% and redirect promotions to weekends to drive volume on those days
2. Engineer the weekday menu toward higher-margin items — promote grills over beverages during lunch hours
3. Implement dynamic time-based pricing with premiums during peak hours (13:00–16:00)
4. Create weekday "business lunch" bundles with better margins than à la carte ordering

---

### 4. Customer Satisfaction — The Rating-Revenue Connection

Average chain-wide rating is **3.70 / 5.0**. Rating directly and measurably correlates with customer lifetime value: Cairo's 4.0 rating drives 8.93 orders per customer, while Assiut's 3.1 rating results in only 2.58 orders. Every 0.1 rating point increase corresponds to approximately **0.7 additional orders per customer**.

**Rating Distribution:**

| Stars | % of Customers | Interpretation |
|-------|---------------|----------------|
| ⭐⭐⭐⭐⭐ 5 stars | 15% | Target: 25–30% for a thriving chain |
| ⭐⭐⭐⭐ 4 stars | 44% | Satisfied but not delighted — at risk of churn |
| ⭐⭐⭐ 3 stars | 36.5% | One bad experience away from leaving permanently |
| ⭐⭐ 2 stars | 4.1% | Lost customers — will not return |
| ⭐ 1 star | ~0.4% | Actively harmful to brand reputation |

**Branch-Level Breakdown:**
- Cairo (4.0 rating): 20.8% give 5 stars, 58.4% give 4 stars — strong, repeatable performance
- Alexandria (3.8 rating): 10% give 5 stars — middle performer with clear upside potential
- Assiut (3.1 rating): Only 0.27% give 5 stars, 65.7% stuck at 3 stars — critical failure state requiring urgent intervention

**Strategic Actions:**
1. Target a **4.2+ average rating chain-wide** — this would increase orders per customer by ~1.4, adding EGP 400M+ in annual revenue
2. Implement a "5-star guarantee" program — if customers do not rate 5 stars, offer 20% off their next visit; this costs far less than acquiring new customers
3. Focus intensively on 3-star converters — 36.5% of customers at this level are the biggest single opportunity; identify pain points through targeted post-visit surveys
4. Branch-specific interventions — Assiut requires a complete operational overhaul; Alexandria needs targeted service training programs

---

### 5. Product Mix Optimization — Untapped Category Potential

**Category Revenue Breakdown:**

| Category | Revenue | Revenue Share | Margin | Status |
|----------|---------|--------------|--------|--------|
| Grills (مشويات) | EGP 1.01B | 34.9% | 3.61% | Cash cow |
| Tagines (طواجن) | EGP 0.81B | 27.9% | 3.61% | Strong performer |
| Poultry (محاشي) | EGP 0.54B | 18.6% | — | Stable |
| Starters (مقبلات) | EGP 0.34B | 11.7% | — | Stable |
| Beverages (مشروبات) | EGP 0.20B | 7.0% | Low | Severely underpriced |

**The Beverage Opportunity:**
- Beverages generate only **EGP 28.37 per unit** despite being a very high-volume category with 7M+ units sold
- Mango Juice alone sold **4.28M units** but generated only EGP 121M — EGP 28.38 per unit
- Tea is the worst performer across the entire menu at just EGP 20M total revenue
- No premium beverage options exist — the chain is entirely missing the EGP 50–80 fresh juice and specialty drink tier
- Beverages are inherently high-margin, low-cost items that should be driving profitability — they are currently being left behind

**Within-Category Insights:**
- Kebab dominates the grill category at 50% of category revenue — premium kebab varieties should be expanded
- Chicken Tagine accounts for 40% of the tagine category — the single most popular dish chain-wide
- Stuffed Eggplant is the weakest performer in stuffed dishes (steepest decline slope at -1.33) — a clear candidate for removal
- Kofta and Molokhia Tagine round out the top 5 revenue-generating items

**Strategic Actions:**
1. Increase beverage prices by 30–40% — raise Mango Juice from EGP 28 to EGP 40–45
2. Introduce a premium beverage tier — fresh-squeezed juices, smoothies, specialty teas at EGP 60–80 (2–3x current prices)
3. Bundle beverages with meals — "Meal + Drink" combos at a slight discount to increase attachment rates
4. Remove the bottom 20% of menu items (Tea, Stuffed Eggplant) and consolidate focus on top performers
5. Expand the Kebab line — add premium varieties (lamb, mixed grill platters) at EGP 200–250
6. Introduce a dessert category — currently entirely absent from the menu; adding it could increase basket size by 15–20% across all order types

---

### 6. Cross-Selling & Basket Size — The Multi-Item Opportunity

**Order Composition Breakdown:**

| Items per Order | % of Orders | Avg Order Value |
|----------------|------------|----------------|
| 1 item | 21.7% | EGP 281 |
| 2 items | 22.8% | EGP 571 |
| 3 items | 16.9% | EGP 813 |
| 6–7 items | 23.1% | EGP 2,200–2,300 |
| 9 items | 0.8% | EGP 2,377 |

- **21.7% of orders** (542,007 transactions) contain only one item — these are typically quick takeaway or delivery orders
- A single-item customer spends EGP 281 vs. EGP 571 for a two-item order — EGP 290 is lost per transaction
- Converting just **50% of single-item orders to two-item orders** = **+EGP 78.6M in additional annual revenue**
- The 6–7 item tier (23.1% of all orders) represents family and group meals averaging EGP 2,200–2,300 — a segment worth protecting and growing
- Current average items per order is only **3.2** — the realistic target should be 4–5 items per order

**Strategic Actions:**
1. Train staff on suggestive selling — recommend an appetizer with every grill order, a drink with every main
2. Update the POS system and ordering app with "Add a Side" and "Complete Your Meal" prompts at checkout
3. Introduce minimum order incentives — "Spend EGP 500, get 10% off" encourages larger basket sizes
4. Create pre-configured family meal bundles (6–7 items) at EGP 2,000 vs. EGP 2,300 à la carte
5. Run a beverage attachment campaign — "Add any drink for EGP 20 with your main course"
6. Add a dessert category — currently absent; this alone could increase per-order basket size by 15–20%

---

### 7. Payment Method & Order Type Insights

**Payment Breakdown:**

| Method | Revenue Share | Revenue | Avg Order Value |
|--------|--------------|---------|----------------|
| Cash | 50% | EGP 1.45B | EGP 260.75 |
| Card | 30% | EGP 0.87B | EGP 261.09 |
| Wallet | 20% | EGP 0.58B | EGP 260.72 |

**The Cash Problem:**
- 50% cash transactions create significant operational inefficiencies — manual counting, security risks, and daily bank deposits
- Cash customers have virtually identical order values to digital customers — there is no natural economic incentive for them to switch
- Cash transactions create a critical data gap — the repeat behavior and preferences of 50% of customers cannot be tracked, making personalization and loyalty programs impossible for half the customer base

**Order Type Breakdown:**

| Order Type | Revenue Share | Revenue |
|-----------|--------------|---------|
| Dine-in | 39.98% | EGP 1.16B |
| Takeaway | 30.03% | EGP 0.87B |
| Delivery | 29.99% | EGP 0.87B |

- All three order types share an identical average rating of 3.70 — no meaningful service quality gap exists between channels
- Dine-in generates the highest total revenue and should be the primary target for experience investment
- Delivery and Takeaway each represent approximately EGP 0.87B — a significant combined base worth optimizing

**Strategic Actions:**
1. Offer 5% cashback for card or wallet payments to shift behavior away from cash
2. Tie the loyalty program exclusively to digital payments — earn points only via card or wallet to create a meaningful incentive
3. Invest in dine-in ambiance and service quality — highest revenue channel and most defensible against delivery aggregator competition
4. Optimize delivery partnerships — negotiate better terms with aggregators and improve delivery times to grow this channel further

---

### 8. Operational Efficiency — Peak Hour Management

**Peak Hour Findings:**
- Wednesday 8PM is the single busiest hour chain-wide (110,989 orders), followed by Saturday 6PM (110,949 orders)
- Weekend afternoons (14:00–15:00) show the highest average order values at EGP 330+ — family lunch occasions dominate
- Weekday lunches (12:00 Monday) average only EGP 177 — quick individual meals with low basket sizes
- The top 20 hour-day combinations account for only **20.5% of total orders** — demand is highly concentrated and fully predictable
- The 13:00–16:00 and 19:00–23:00 windows account for approximately **70% of all daily orders**
- Cairo dominates every single slot in the peak hours table — branches 2 through 6 never appear in the top tier, suggesting severe capacity underutilization at non-Cairo locations during peak periods

**The Capacity Problem:**
- The chain is almost certainly understaffed during off-peak hours and overwhelmed during peak periods
- Peak hour congestion drives longer wait times, which directly suppresses customer ratings across all branches
- Predictable demand patterns mean this is entirely solvable with scheduling optimization

**Strategic Actions:**
1. Implement dynamic staffing — increase staff by 40% during 13:00–16:00 and 19:00–23:00; reduce by 30% during 10:00–12:00 and 17:00–18:00
2. Launch off-peak "Happy Hour" promotions — 20% off between 10:00–12:00 and 17:00–18:00 to smooth and redistribute demand
3. Introduce a pre-ordering system — allow customers to place orders 30+ minutes in advance during known peak windows
4. Expand kitchen capacity specifically for peak-hour items — add prep stations for Kebab and Chicken Tagine which dominate peak period orders
5. Throttle delivery orders during peak dine-in hours to protect higher-value in-restaurant customers from experiencing degraded service

---

## 🎯 Strategic Recommendations Roadmap

### Immediate Actions (0–3 Months)

| Action | Detail | Estimated Annual Impact |
|--------|--------|------------------------|
| Fix Assiut or Exit | Full operational audit; replace management if needed; close within 90 days if no improvement | +EGP 50M |
| Optimize Weekday Pricing | Reduce weekday discounts from 2.59% to 1.5%; introduce premium lunch bundles at EGP 150–180; implement peak-hour dynamic pricing | +EGP 35M |
| Launch Cross-Sell Campaign | Train staff on suggestive selling; add POS/app "Complete Your Meal" prompts; minimum order incentives | +EGP 80M |
| Raise Beverage Prices | Increase by 35% (EGP 28 → EGP 40); add premium fresh juice tier at EGP 60–80; bundle beverages with mains | +EGP 40M |

### Medium-Term Initiatives (3–12 Months)

| Action | Detail | Estimated Annual Impact |
|--------|--------|------------------------|
| Cairo Expansion | Open 2–3 new Cairo locations in high-traffic office districts and shopping centers | +EGP 300M |
| Customer Experience Overhaul | "5-star guarantee" program; upgrade Assiut, Tanta, Mansoura facilities; monthly customer feedback loops with action plans | +EGP 400M |
| Digital Transformation | Shift 50% of cash to digital via 5% cashback incentive; launch loyalty mobile app; implement CRM for personalized marketing | +EGP 100M |
| Menu Innovation | Add dessert category; introduce premium grill platters at EGP 200–250; remove bottom 20% of menu items | +EGP 150M |

### Long-Term Strategy (12+ Months)

| Action | Detail | Estimated Annual Impact |
|--------|--------|------------------------|
| Geographic Expansion | Enter new cities with Cairo-like demographics; franchise model for rapid scaling; target 15–20 locations within 3 years | +EGP 500M |
| Brand Repositioning | Shift from affordable Egyptian food to premium traditional cuisine; upgrade interiors, plating, and service standards to justify 15–20% price increases | +20% pricing headroom |

---

## 🛠️ Tech Stack

| Tool | Role |
|------|------|
| **Databricks** | Cloud data platform — DBFS storage and Spark SQL compute engine |
| **Apache Spark** | Distributed processing of 1.5 GB / 11M rows across 9 source files |
| **Delta Lake** | Reliable managed storage layer on top of DBFS |
| **Spark SQL** | Data merging via multi-table JOINs, transformation, and field enrichment |
| **Power BI** | 4-page interactive dashboard with 6 cross-filter slicers |
| **Partner Connect** | Live Databricks → Power BI direct connection |

---

## 🚀 How to Reproduce

### Prerequisites
- Databricks account (Community Edition or higher)
- Power BI Desktop
- The 9 source data files

### Steps

1. **Upload data to DBFS**
   Navigate to: `Databricks UI → Data → Add Data → Upload Files`
   Target path: `dbfs:/FileStore/restaurant/`

2. **Run the Spark SQL merge pipeline**
   Open a new Databricks SQL Notebook, load all 9 source files as tables, then run the JOIN-based unification to produce the master analytical table (~11M rows)

3. **Connect Power BI to Databricks**
   In Power BI Desktop: `Get Data → Databricks`
   Enter your server hostname and HTTP path, then select the master table

4. **Open and refresh the dashboard**
   Open `powerbi/restaurant_dashboard.pbix` and refresh credentials if prompted

---

## 👤 Author

Built as a personal end-to-end data engineering and analytics project, demonstrating full pipeline design from raw multi-source data ingestion through Databricks to executive-level Power BI business intelligence.

---

## 📄 License

This project is licensed under the MIT License.

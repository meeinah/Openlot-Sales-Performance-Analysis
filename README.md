# Openlot E-commerce Sales & Performance Analysis

## Project Background  
Openlot Retail, established in 2014, is a global e-commerce retailer specializing in the sale of fast-moving consumer goods (FMCG).  
As a data analyst at Openlot, I was tasked with creating an operational analytics package for Executives, Sales, Operations, and Finance to provide clear visibility into sales trends, product performance, regional performance, customer behavior, and payment patterns across 2014–2021.  

The dataset used for this analysis contains ~1,000,000 rows across six dimension/fact tables and covers the period from 2014 through 2021.  

**Key business metrics:**  
- Total Revenue  
- Quantity (units sold)  
- Active Customers  
- Average Unit Price (AUP)  

**Audience/Stakeholders:** Executives (CEO/CFO), Head of Sales, Head of Operations, Head of Supply Chain, Finance Manager, and Regional Managers  

**Insight Areas of this report):**  
- Overall Performance (monthly KPIs, YoY growth, Average Unit Price)  
- Product Performance (top units/categories)  
- Customer Insights (top customers, payment methods)  
- Regional & Global Performance (top countries, store divisions)  
- Supply Chain Insights (top suppliers)  

**The Excel queries, pivot models used for cleaning, and the dashboard can be found [here](https://drive.google.com/drive/folders/1tiDSgRcvXFr_uyY02QFXaEeMCuXdW-_Y?usp=drive_link)**  

---

## Data Structure & Initial Checks  

The company's main database consists of six tables, with a total row count of ~1 million.  

**Tables (source CSVs):**  
- **customer_dim.csv** — `customer_key, name, contact_no, nid`  
  *Purpose: customer master table.*  

- **fact_table.csv** — `payment_key, customer_key, time_key, item_key, store_key, quantity, unit, unit_price, total_price`  
  *Purpose: transaction-level facts.*  

- **item_dim.csv** — `item_key, item_name, desc, unit_price, man_country, supplier, unit`  
  *Purpose: product master, including supplier and manufacturer country.*  

- **store_dim.csv** — `store_key, division, district, upazila`  
  *Purpose: store geography / regional attributes.*  

- **time_dim.csv** — `time_key, date, hour, day, week, month, quarter, year`  
  *Purpose: canonical time attributes for trend analysis.*  

- **trans_dim.csv** — `payment_key, trans_type, bank_name`  
  *Purpose: payment/transaction channel details (card, mobile, cash, etc.).*  

**Initial Checks:**  
- Rowcounts matched source CSVs (~1M total).  
- Date coverage validated: **2014–2021**.  
- Key joins validated:  
  - `fact_table` → `customer_dim` (customer_key)  
  - `fact_table` → `item_dim` (item_key)  
  - `fact_table` → `store_dim` (store_key)  
  - `fact_table` → `time_dim` (time_key)  
  - `fact_table` → `trans_dim` (payment_key)  
- Null checks completed for critical fields (`total_price, quantity, unit_price, time_key`).  
- Small number of refunds/dates cleaned or excluded.  

  <img width="1132" height="556" alt="entity rel openlot" src="https://github.com/user-attachments/assets/98cec2ac-a74b-4b35-b794-84ec31e6b449" />


---

## Executive Summary  

### Overview of Findings  
Overall sales and volume have been stable across months with steady revenue growth driven by price/volume mix rather than new customer acquisition. Total reported revenue stands at $105M, total quantity 6M units, and total customers 9.2K. A small set of products, customers, suppliers and regions account for a disproportionate share of revenue and units — prioritizing these high-performing segments will deliver the greatest near-term lift.

<img width="1030" height="509" alt="dash" src="https://github.com/user-attachments/assets/75a2e0b1-4bae-42e6-8d82-bb3f457a7a18" />


---

## Insights Deep Dive

### Overall Performance
- **Total revenue** reached **$105M**, **total quantity** 6M, and **total customers** 9.2K.  
- Month-to-month performance between **2014 and 2021** remained stable, with minor dips in **February** and peaks in **May**, indicating consistent seasonal patterns.  
- **Revenue and quantity** increased by **16.12% YoY**, but **customer growth** remained flat at 0%, showing that growth was driven by **existing customers** and **higher sales per customer** rather than acquisition.  
- The **average unit price** held steady at **$18** across all years, reflecting a consistent pricing strategy that supported stability without heavy reliance on price changes.  
- Most of the revenue is concentrated in **specific customers, products, and regions**, highlighting dependency on top performers.  

![kpi tracking (3)](https://github.com/user-attachments/assets/c8e556f7-36fd-44a0-9f07-dd944008f623)


### Product Performance
- Units measured in **Ct (39.4%)** and **Cans (21.6%)** dominated sales, accounting for over **60% of all units sold**.  
- **Beverage – Energy/Protein** and **Food – Healthy** categories contributed nearly **20% of total revenue**, making them essential to profitability and branding.  
- A few **SKUs consistently drove the majority of revenue** each year, showing limited product diversification and dependence on category leaders.  
- Category performance remained steady across the years without significant shifts in consumer demand, indicating **predictable supply chain trends**.  

![kpi tracking (2)](https://github.com/user-attachments/assets/5b8a2059-81f6-4c98-9533-a1dcf2c7d1c2)


### Customer Insights
- **Customer Pooja** consistently purchased nearly **double the units** of the second-highest customer, making her the **most valuable customer** over the full period.  
- Despite revenue growth, **customer count stagnated** at ~9.2K across 2014–2021, meaning **retention and cross-sell** strategies were more effective than acquisition.  
- **Card payments** dominated at **89.7%**, while **mobile and cash payments** made up a minimal share, showing heavy reliance on card channels.  
- Minimal adoption of alternative payment methods indicates an opportunity to **incentivize mobile wallet use** to diversify payments.  

![kpi tracking](https://github.com/user-attachments/assets/c2961bfe-bebb-42bd-ac83-6e7e3d1e44be)


### Regional & Supply Chain Performance
- **Bangladesh and India** contributed more than **25% of global sales revenue**, making them the top-performing countries.  
- Domestically, **Dhaka (38.7%)** and **Chittagong (18.8%)** consistently led sales, together accounting for **over half of division-level performance**.  
- **DENIMACH LTD, Indo Count, and Friedola 1888** remained the **top three suppliers** across the period, dominating supply volumes.  
- Revenue concentration in a **handful of regions and suppliers** created both opportunities and risks — any disruption could significantly affect total revenue.  

![kpi tracking (1)](https://github.com/user-attachments/assets/ccee78fe-f68e-4732-b116-397a43e6d771)


---

## Recommendations  

#### Product Strategy  
- Continue prioritizing high-volume units (**Ct and Cans**) and high-revenue categories (**Beverage – Energy/Protein, Food – Healthy**).  
- Explore opportunities to refresh or bundle underperforming products to balance category performance.  

#### Customer Engagement  
- Strengthen loyalty programs for top customers like **Pooja**, focusing on personalized offers and retention.  
- Invest in customer acquisition strategies to complement revenue growth, since YoY customer growth is flat.  

#### Regional Expansion  
- Allocate more resources to **Dhaka, Chittagong, Bangladesh, and India**, given their dominant contribution to sales.  
- Explore growth opportunities in underperforming regions to reduce overreliance on a few markets.  

#### Payments & Financial Strategy  
- Encourage **mobile wallet adoption** through promotions and partnerships to reduce dependency on card payments.  
- Monitor payment trends to align financial operations with evolving consumer behaviors.  

#### Supply Chain Management  
- Strengthen partnerships with dominant suppliers (**DENIMACH LTD, Indo Count, Friedola 1888**) to secure consistent inventory.  
- Diversify supplier base slightly to mitigate risks of over-dependence.

---

## Assumptions & Caveats  
- **Date coverage:** Analysis includes **2014–2021** only.  
- **Missing/messy data:** Refunds & non-sensical dates excluded. Missing Dec 2021 not imputed.  
- **Currency:** All revenue reported in USD.  
- **Unit-price calc:** `total_price = unit_price * quantity`.  
- **Customer identity:** Names assumed unique; multiple accounts may bias top-customer analysis.  
- **Geography source:** Used `item_dim.man_country` where customer country missing.  
- **Payments:** Relied on `trans_dim.trans_type` — unmapped/null excluded.  

---

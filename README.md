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

📌 *Entity Relationship Diagram available here.*  

---

## Executive Summary  

### Overview of Findings  
Overall sales and volume have been stable across months with steady revenue growth driven by price/volume mix rather than new customer acquisition.  
- **Total Revenue:** $105M  
- **Total Quantity:** 6M units  
- **Total Customers:** 9.2K  

A small set of products, customers, suppliers, and regions account for a disproportionate share of revenue and units — prioritizing these high-performing segments will deliver the greatest near-term lift.  

---

## Insights Deep Dive  

### Overall Performance  
- Revenue reached **$105M**, quantity **6M**, and customers **9.2K** (2014–2021).  
- Month-to-month performance remained stable with dips in **February** and peaks in **May**.  
- **YoY growth:** Revenue & quantity up **16.12%**, customers flat at **0%** → growth driven by existing customers.  
- **Average Unit Price:** Steady at **$18**, showing a stable pricing strategy.  

---

### Product Performance  
- **Top Units:** Ct (**39.4%**) and Cans (**21.6%**) accounted for >60% of all units sold.  
- **Top Categories:** Beverage – Energy/Protein and Food – Healthy contributed ~20% of total revenue.  
- Few SKUs consistently dominated revenue → dependence on category leaders.  
- Consumer demand stable across years → predictable trends for supply chain.  

---

### Customer Insights  
- **Top Customer:** Pooja consistently purchased nearly double the units of the 2nd-highest customer.  
- **Customer Growth:** Stagnant at ~9.2K (2014–2021). Retention > acquisition.  
- **Payments:** Card = **89.7%** of transactions; mobile & cash minimal.  
- Opportunity: Incentivize **mobile wallets** to diversify adoption.  

---

### Regional & Supply Chain Performance  
- **Top Countries:** Bangladesh & India contributed >25% of global revenue.  
- **Domestic Leaders:** Dhaka (**38.7%**) and Chittagong (**18.8%**) dominated division sales.  
- **Top Suppliers:** DENIMACH LTD, Indo Count, Friedola 1888 led across all years.  
- Revenue concentration in few regions & suppliers → both opportunity and risk.  

---

## Recommendations  

**Product Strategy**  
- Continue prioritizing **Ct and Cans**, and high-revenue categories.  
- Refresh/bundle underperforming products to balance category performance.  

**Customer Engagement**  
- Strengthen loyalty programs for top customers (e.g., Pooja).  
- Invest in **customer acquisition** to complement revenue growth.  

**Regional Expansion**  
- Prioritize Dhaka, Chittagong, Bangladesh, India.  
- Explore growth in underperforming markets.  

**Payments & Finance**  
- Promote **mobile wallets** via discounts/partnerships.  
- Track evolving consumer payment preferences.  

**Supply Chain Management**  
- Strengthen partnerships with top suppliers.  
- Diversify supplier base to reduce over-dependence.  

---

## Assumptions & Caveats  
- **Date coverage:** Analysis includes **2014–2021** only.  
- **Missing/messy data:** Refunds & non-sensical dates excluded. Missing Dec 2021 not imputed.  
- **Currency:** All revenue reported in USD (or supplied currency).  
- **Unit-price calc:** `total_price = unit_price * quantity`.  
- **Customer identity:** Names assumed unique; multiple accounts may bias top-customer analysis.  
- **Geography source:** Used `item_dim.man_country` where customer country missing.  
- **Payments:** Relied on `trans_dim.trans_type` — unmapped/null excluded.  

---

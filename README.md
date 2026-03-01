# 🍦 Baskin Robbins Sales Dashboard — Power BI Mini Project 2

## 📁 Dataset Overview

| Sheet | Description | Records |
|---|---|---|
| **Bills** | Sales transactions with date, payment, category, GST | 50,000 rows |
| **Outlet** | Store details — name, city, state, manager | 270 stores |
| **Product** | Product catalog with categories and pricing | 144 products |
| **statehead** | State-level head/manager mapping | 6 states |

Key Dimensions:
- 🗓️ Date Range: 2020 – 2025
- 🏪 270 Outlets across multiple Indian states
- 🍨 13 Product Categories
- 💳 5 Payment Modes: UPI, Cash, Card, Digital Wallet, Gift Coupons

---

## 🛠️ Tools & Technologies

- **Power BI Desktop** — Dashboard creation and visualization
- **Power Query** — Data cleaning and transformation
- **DAX** — Custom measures and calculations
- **Excel (.xlsx)** — Source data format

---

## 🔧 Power Query Steps Applied

- Changed data types for Date, Amount, and Quantity columns
- Renamed columns (fixed typo: Oder_day → Order_day)
- Removed unnecessary/unnamed columns from Product table
- Standardized Store_id column across Bills and Outlet tables for relationship

---

## 🔗 Data Model — Table Relationships

Bills[Store_id]  →  Outlet[Store_id]    (Many-to-One)
Bills[Category]  →  Product[Category]   (Many-to-One)
Outlet[State]    →  statehead[state]    (Many-to-One)

---

## 📐 DAX Measures Created

Total Revenue = SUM(Bills[Grand_total])

Total Orders = DISTINCTCOUNT(Bills[Order Id])

Total Quantity Sold = SUM(Bills[Quantity])

Average Order Value = DIVIDE([Total Revenue], [Total Orders])

Total Discount Given = SUM(Bills[Discount])

Total GST Collected = SUM(Bills[GST])

Revenue per Item = DIVIDE([Total Revenue], [Total Quantity Sold])

Avg Revenue per Store = DIVIDE([Total Revenue], DISTINCTCOUNT(Bills[Store_id]))

Total Stores = DISTINCTCOUNT(Bills[Store_id])

YTD Revenue = TOTALYTD([Total Revenue], Bills[Bill_date])

MOM Revenue Growth % =
VAR CurrentMonthSales = CALCULATE(SUM(Bills[Grand_total]))
VAR PrevMonthSales = CALCULATE(
    SUM(Bills[Grand_total]),
    PREVIOUSMONTH(Bills[Bill_date])
)
RETURN
DIVIDE(CurrentMonthSales - PrevMonthSales, PrevMonthSales)

---

## 📈 Dashboard Visuals

| Visual | Type | Fields Used |
|---|---|---|
| Total Revenue | KPI Card | Total Revenue |
| Avg Order Value | KPI Card | Average Order Value |
| Total Orders | KPI Card | Total Orders |
| Total Qty Sold | KPI Card | Total Quantity Sold |
| Monthly Revenue Trend | Line Chart | Order_month × Total Revenue |
| Revenue by Category | Bar Chart | Category × Total Revenue |
| Revenue by Payment Mode | Donut Chart | Payment Mode × Total Revenue |
| Top 5 Stores by Revenue | Bar Chart | Store Name × Total Revenue + Top N Filter |
| Category Slicer | Slicer | Bills[Category] |
| Year Slicer | Slicer | Bills[order_year] |

---

## 🔍 Key Findings

- 📌 Total Revenue: 24.48M across all outlets and years
- 📌 Ice Cream Cakes lead category revenue at 8.3M
- 📌 Average Order Value: ₹503 with 49K total orders
- 📌 Gift Coupons are the most used payment mode at 29.32%
- 📌 150K total quantity sold across all 13 categories
- 📌 Revenue is fairly evenly distributed across payment modes — showing diverse customer preferences

---


This is Mini Project 2 of my Data Analytics training.
Mini Project 1 was built on the Amazon Best Sellers Dataset (2009–2019).

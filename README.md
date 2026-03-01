# 🍦 Baskin Robbins Sales Dashboard — Power BI Mini Project 2

![Power BI](https://img.shields.io/badge/Power%20BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-0078D4?style=for-the-badge&logo=microsoft&logoColor=white)
![Excel](https://img.shields.io/badge/Excel-217346?style=for-the-badge&logo=microsoftexcel&logoColor=white)

> A one-page interactive sales dashboard built using Power BI as part of my Data Analytics training at Global Quest Technologies.

---

## 📊 Dashboard Preview

*(Add your dashboard screenshot here)*

---

## 📁 Dataset Overview

| Sheet | Description | Records |
|---|---|---|
| **Bills** | Sales transactions with date, payment, category, GST | 50,000 rows |
| **Outlet** | Store details — name, city, state, manager | 270 stores |
| **Product** | Product catalog with categories and pricing | 144 products |
| **statehead** | State-level head/manager mapping | 6 states |

**Key Dimensions:**
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
- Renamed columns (fixed typo: `Oder_day` → `Order_day`)
- Removed unnecessary/unnamed columns from Product table
- Standardized `Store_id` column across Bills and Outlet tables for relationship

---

## 🔗 Data Model — Table Relationships

```
Bills[Store_id]     →  Outlet[Store_id]      (Many-to-One)
Bills[Category]     →  Product[Category]     (Many-to-One)
Outlet[State]       →  statehead[state]      (Many-to-One)
```

---

## 📐 DAX Measures Created

```DAX
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
```

---

## 📈 Dashboard Visuals

| Visual | Type | Fields Used |
|---|---|---|
| Total Revenue | KPI Card | `[Total Revenue]` |
| Avg Order Value | KPI Card | `[Average Order Value]` |
| Total Orders | KPI Card | `[Total Orders]` |
| Total Qty Sold | KPI Card | `[Total Quantity Sold]` |
| Monthly Revenue Trend | Line Chart | `Order_month` × `[Total Revenue]` |
| Revenue by Category | Bar Chart | `Category` × `[Total Revenue]` |
| Revenue by Payment Mode | Donut Chart | `Payment Mode` × `[Total Revenue]` |
| Top 5 Stores by Revenue | Bar Chart | `Store Name` × `[Total Revenue]` + Top N Filter |
| Category Slicer | Slicer | `Bills[Category]` |
| Year Slicer | Slicer | `Bills[order_year]` |

---

## 🔍 Key Findings

- 📌 **Total Revenue: 24.48M** across all outlets and years
- 📌 **Ice Cream Cakes** lead category revenue at **8.3M**
- 📌 **Average Order Value: ₹503** with 49K total orders
- 📌 **Gift Coupons** are the most used payment mode at **29.32%**
- 📌 **150K total quantity** sold across all 13 categories
- 📌 Revenue is fairly **evenly distributed** across payment modes — showing diverse customer preferences

---

## 📂 Repository Structure

```
📦 baskin-robbins-powerbi-dashboard
 ┣ 📊 baskin_robbins_dashboard.pbix   ← Power BI file
 ┣ 📂 data/
 ┃ ┗ 📄 baskin_robbins_new.xlsx       ← Source dataset
 ┣ 📸 dashboard_screenshot.png        ← Dashboard preview image
 ┗ 📄 README.md                       ← You are here
```

---

## 🚀 How to Use

1. Clone or download this repository
2. Open `baskin_robbins_dashboard.pbix` in **Power BI Desktop**
3. If data doesn't load, go to **Transform Data → Data Source Settings** and update the path to `baskin_robbins_new.xlsx`
4. Explore the dashboard using the **Category** and **Year** slicers

---

## 🙏 Acknowledgements

Grateful to **Global Quest Technologies** for consistently providing valuable practical exposure, and deeply thankful to **G.R Narendra Reddy Sir** for his guidance, motivation, and unwavering support throughout this journey.

---

## 🔗 Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](your-linkedin-url-here)

---

*This is Mini Project 2 of my Data Analytics training. Mini Project 1 was built on the Amazon Best Sellers Dataset (2009–2019).*

# 📊 Retail Sales, Returns & Anomaly Analysis (Power BI)

## 🧠 Project Overview
This project analyzes **retail transactional data** to understand **sales performance, returns, cancellations, customer behavior, and revenue anomalies**.  
The goal is to move beyond basic KPIs and identify **risk patterns, operational inefficiencies, and abnormal customer or date-level behavior** using **Power BI**.

The analysis focuses on:
- Net Revenue trends
- Sales vs Returns vs Cancellations
- Customer-level anomalies
- Product performance
- Country-level drill-through insights
- Revenue anomaly detection over time

---

## 🗂️ Dataset Description
The dataset contains **invoice-level retail transactions** with the following key fields:

| Column | Description |
|------|------------|
| InvoiceNo | Unique invoice identifier |
| InvoiceDate | Date of transaction |
| CustomerID | Customer identifier |
| StockCode | Product code |
| Description | Product name |
| Quantity | Quantity sold (negative = return) |
| UnitPrice | Price per unit |
| Country | Customer country |

### Important Notes
- **Cancelled invoices** are identified by negative quantities.
- All **returns are cancelled invoices**, but not all cancelled invoices represent revenue loss.
- Zero-priced products are treated separately to avoid revenue distortion.

---

## 🧹 Data Cleaning (Power Query)
Data cleaning was performed **before loading into Power BI**, focusing on:

✔ Removed corrupted rows  
✔ Fixed shifted columns  
✔ Converted data types correctly  
✔ Separated **Active vs Cancelled invoices**  
✔ Handled zero-priced products  
✔ Ensured Quantity sign consistency  

**Flags Created:**
- `Invoice_Status` → Active / Cancelled
- `Quantity_Flag` → Sale / Return
- `Price_Flag` → Normal / Zero / Anomaly

> Cleaning was done in **Power Query** to ensure model stability and accurate DAX results.

---

## 🧮 Key Business Logic
### Definitions Used
- **Sales** → Only positive quantity invoices
- **Returns** → Negative quantity invoices
- **Net Revenue** → Revenue from active (non-cancelled) invoices only
- **Cancelled Orders** → Orders with return quantities
- **Return Rate** → Returned quantity ÷ (Sold + Returned quantity)

---

## 📌 KPIs Created
| KPI | Description |
|---|---|
| Total Quantity Sold | Sum of all positive quantities |
| Net Revenue | Revenue excluding returns |
| Total Orders | Distinct invoice count |
| Cancelled Orders | Count of cancelled invoices |
| Cancelled % | Cancelled orders ÷ total orders |
| Total Customers Bought | Customers with at least one active order |
| Average Order Value (AOV) | Net Revenue ÷ Total Orders |
| Total Returned Amount | Value of returned items |
| Total Quantity Returned | Absolute sum of returned quantities |

---

## 📈 Dashboard Structure
### 1️⃣ Main Dashboard
- KPI cards for overall performance
- Monthly order trend
- Net Revenue by Country
- Interactive slicers for **Country** and **Year**
- Drill-through enabled for deeper analysis

## 📷 Dashboard Preview
![Dashboard](Images/dashboard_overview.png)

### 2️⃣ Country Drill-through Page
- Displays selected country dynamically
- Product-level performance
- Parameter-based metric switching:
  - Net Revenue
  - Quantity Sold
  - Quantity Returned
  - Returned Amount
  - Zero-priced products
## Country Drill-Through Analysis
![Country Drillthrough](images/country_drillthrough.png)

### 3️⃣ Anomaly Detection – Time Series
- **Net Revenue by Date** line chart
- Power BI anomaly detection enabled
- Identifies **unusual spikes and drops**
- Drill-through to date-level detail table
![Customer Anomalies](images/customer_anomalies.png)

### 4️⃣ Customer Anomaly Detection Table
Customer-level metrics used to identify risky or abnormal behavior:
- Total Orders
- Positive Orders
- Cancelled Orders
- Cancelled %
- Total Returned Amount
![Customer Anomalies](images/customer_anomalies.png)

Conditional formatting highlights:
- 🔴 High cancellation percentage
- 🟡 Medium risk customers
- 🟢 Low risk customers

---

## 🚨 Anomaly Detection Logic
### Time-Based Anomalies
Detected when:
- Revenue spikes significantly above historical trend
- Revenue drops unexpectedly
- Seasonal deviations exceed confidence band

**Use Case:**
- Promotion impact
- Bulk orders
- Data quality issues
- Fraud or operational issues

### Customer-Level Anomalies
Identified customers with:
- High cancellation %
- High returned amount
- Disproportionate order behavior

**Use Case:**
- Fraud detection
- Policy abuse
- Customer profitability analysis

---

## 💡 Key Insights
- A small number of customers contribute **disproportionately to cancellations**
- Revenue spikes are **not always sustainable growth**
- Certain products drive **high returns despite strong sales**
- Country-level performance varies significantly
- Zero-priced products can distort quantity-based KPIs if not isolated

---

## 📌 Business Recommendations
1️⃣ **Flag High-Risk Customers**
- Monitor customers with >30% cancellation rate
- Introduce stricter return policies or manual review

2️⃣ **Product-Level Quality Review**
- Investigate high-return products
- Improve descriptions or quality checks

3️⃣ **Revenue Spike Validation**
- Validate abnormal revenue days for promotions or errors
- Avoid overestimating growth from one-off events

4️⃣ **Operational Improvements**
- Reduce cancellations by improving order accuracy
- Introduce pre-shipment checks for high-return customers

5️⃣ **Better Forecasting**
- Use cleaned net revenue trends for forecasting
- Exclude anomaly days from baseline models

---

## 🛠️ Tools Used
- **Power BI**
- **Power Query**
- **DAX**
- **Excel (initial data inspection)**

---

## 📄 Full Report
[Download PDF Report](Report/Retail_KPI_Anomaly_Report.pdf)



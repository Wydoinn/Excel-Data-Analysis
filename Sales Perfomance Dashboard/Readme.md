# 🛒 Sales Performance Dashboard

This project analyzes FMCG daily sales data (2022–2024) using **Excel Power Query, Power Pivot, DAX, and PivotTables**. The goal was to design an interactive dashboard to track sales, promotions, stock, and delivery performance across regions and channels.

![Demo](https://github.com/user-attachments/assets/afda61d7-427b-41e9-aa9f-4c3a885e6ed7)


## 📂 Dataset

Dataset Link: [FMCG Daily Sales Data (2022–2024)](https://www.kaggle.com/datasets/beatafaron/fmcg-daily-sales-data-to-2022-2024)

Columns used:

* `date` → Transaction date
* `region` → Region of sale
* `channel` → Sales channel (Retail, Discount, E-commerce)
* `sku`, `brand` → Product identifiers
* `units_sold` → Units sold
* `price_unit` → Price per unit
* `promotion_flag` → Promotion indicator (0/1)
* `stock_available` → Stock level available
* `delivered_qty` → Delivered quantity
* `delivery_days` → Delivery lead time in days


## ⚙️ Steps Performed

### 1. Data Preparation

* Loaded CSV into **Power Query** and enabled *Load to Data Model*.
* Cleaned columns and ensured correct data types.
* Created DAX measures in **Power Pivot**.

### 2. KPI Cards

Built KPI cards for:

* **Total Revenue**
* **Total Units Sold**
* **Average Price per Unit**
* **Promotion Sales %**
* **Average Delivery Days**

Each card dynamically updates with slicers for **Region, Channel, and Date**.

### 3. PivotTables & Charts

#### 📊 A) Sales Trend (Time Series)

* **Rows**: `date` (grouped by Month/Year)
* **Values**: Total Revenue, Units Sold
* **Chart**: Line Chart

<img width="297" height="282" alt="Screenshot 2025-09-05 133757" src="https://github.com/user-attachments/assets/15d141f7-381a-41e2-9106-126e6aff62d0" />

#### 📊 B) Sales by Region & Channel

* **Rows**: `region`
* **Columns**: `channel`
* **Values**: Revenue or Units Sold
* **Chart**: Clustered Column

<img width="493" height="119" alt="Screenshot 2025-09-05 133806" src="https://github.com/user-attachments/assets/35ee78f0-373a-407b-8b44-9c0f050b16b3" />

#### 📊 C) Top SKUs / Brands

* **Rows**: `sku` or `brand`
* **Values**: Revenue, Units Sold
* **Chart**: Horizontal Bar (sorted descending)

<img width="310" height="315" alt="Screenshot 2025-09-05 133821" src="https://github.com/user-attachments/assets/fb9fad05-5ade-495c-9869-27628b18dbd7" />


#### 📊 D) Promotion Impact

* **Rows**: `promotion_flag`
* **Values**: Units Sold, Revenue
* **Chart**: Column Chart (Promo vs Non-Promo)

<img width="308" height="81" alt="Screenshot 2025-09-05 133828" src="https://github.com/user-attachments/assets/76f41952-879b-49ce-adb2-254ed81fd173" />

#### 📊 E) Stock vs Delivered vs Sold

* **Rows**: `date` (monthly)
* **Values**: Avg Stock Available, Total Delivered Qty, Units Sold
* **Chart**: Combo Chart (Line = Units Sold, Columns = Stock & Delivered)

<img width="461" height="102" alt="Screenshot 2025-09-05 133836" src="https://github.com/user-attachments/assets/cfe2ee8d-c8e4-4ec4-881d-dcca12128315" />

### 4. Dashboard Design

* KPI cards on top row
* Charts arranged in a clean 2×3 grid
* Consistent formatting & colors
* Slicers for quick filtering

<img width="1452" height="658" alt="Screenshot 2025-09-05 133618" src="https://github.com/user-attachments/assets/d14bfdea-d585-48fe-b497-0d446e7dc30a" />


## 🔢 DAX Measures

### Sales Metrics

```DAX
Total Revenue = SUMX(YourTable, [units_sold] * [price_unit])
Total Units Sold = SUM([units_sold])
Average Price = AVERAGE([price_unit])
```

### Promotion & Stock Metrics

```DAX
Promotion Sales % =
DIVIDE(
    SUMX(FILTER(YourTable, [promotion_flag] = 1), [units_sold]),
    SUM([units_sold]),
    0
) * 100

Stock-out % =
DIVIDE(
    COUNTROWS(FILTER(YourTable, [stock_available] = 0)),
    COUNTROWS(YourTable),
    0
) * 100
```

### Delivery Metrics

```DAX
Avg Delivery Days = AVERAGE([delivery_days])
Avg Stock Available = AVERAGE([stock_available])
Total Delivered Qty = SUM([delivered_qty])
```

## ✅ Conclusion

This project demonstrates how **Excel + DAX** can turn raw FMCG sales data into a powerful retail dashboard. With KPI cards, PivotCharts, and slicers, business users can quickly track revenue, stock, promotions, and delivery performance.



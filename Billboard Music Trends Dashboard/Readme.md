# 🎶 Billboard Music Trends Dashboard

An interactive Excel dashboard analyzing **Billboard chart performance** across decades, artists, and songs. This project showcases **data cleaning, transformation, PivotTables, PivotCharts, and slicers** to create insights from raw Billboard chart data.

![Demo](https://github.com/user-attachments/assets/b7478bf8-c765-44c3-9188-1ba74ab7738b)

## ⚙️ Steps Performed

### 1. Data Preparation
- Combined **5 Billboard CSV files** into one refreshable table using **Power Query**.
- Cleaned data:
  - Converted `Weeks_in_chart` column to **Whole Number**.
  - Replaced `null` values with `0`.
  - Added calculated columns:
    - `Is_New` → marks first-time entries.
    - `Decade` → derived from `Year` (`=INT([@Year]/10)*10`).

### 2. PivotTables & Charts
Built **4 major PivotTables** to extract insights:

#### 📊 A) New Entries Per Year
- **Rows**: `Year`  
- **Values**: Count of `Song`  
- **Filter**: `Is_New = Yes`  
- Chart: Column Chart  

#### 📊 B) Average Weeks on Chart (by Decade)
- **Rows**: `Decade`  
- **Columns**: `Chart`  
- **Values**: Average of `Weeks_in_chart`  
- Chart: Clustered Column  

#### 📊 C) Top Artists by #1 Hits
- **Rows**: `Artist`  
- **Values**: Count of `Rank`  
- **Filter**: `Rank = 1`  
- Sorted by Top 10  
- Chart: Horizontal Bar  

#### 📊 D) Song Longevity Distribution
- **Rows**: `Weeks_in_chart` (grouped into ranges: 1–5, 6–10, 11–20…)  
- **Values**: Count of `Song`  
- Chart: Line Chart  

### 3. Dashboard Design
- Created **Dashboard sheet**:
  - Title: *“Billboard Music Trends Dashboard”*.
  - Added **slicers** for `Year`, `Decade`, `Chart`, `Artist`.
  - Connected slicers to all PivotTables.
  - Arranged charts in a **2x2 grid** for readability.
- Applied consistent formatting, colors, and chart titles.

# 🎶 Billboard Music Trends Dashboard

This project combines and analyzes multiple Billboard chart datasets (Billboard 200, Hot 100, Radio, Streaming, Digital) using Power Query & Excel. The goal was to create a unified dataset for exploring music trends, rankings, and song longevity across charts.

![Demo](https://github.com/user-attachments/assets/b7478bf8-c765-44c3-9188-1ba74ab7738b)

## 📂 Datasets
Dataset Link: [Billboard Hot 100 & More](https://www.kaggle.com/datasets/ludmin/billboard)
- Billboard200.csv
- Hot100.csv
-  Radio.csv
- Streaming.csv
- Digital.csv

Each dataset contained Date, Song, Artist, Rank, Last Week, Peak Position, Weeks in Charts.

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

<img width="684" height="306" alt="Screenshot 2025-08-29 152433" src="https://github.com/user-attachments/assets/b56b2521-ea7c-43f9-be68-a342779aea6f" />

#### 📊 B) Average Weeks on Chart (by Decade)
- **Rows**: `Decade`  
- **Columns**: `Chart`  
- **Values**: Average of `Weeks_in_chart`  
- Chart: Clustered Column  

<img width="691" height="314" alt="Screenshot 2025-08-29 152442" src="https://github.com/user-attachments/assets/098b8cd2-4244-4bb6-8577-7638e43fd138" />

#### 📊 C) Top Artists by #1 Hits
- **Rows**: `Artist`  
- **Values**: Count of `Rank`  
- **Filter**: `Rank = 1`  
- Sorted by Top 10  
- Chart: Horizontal Bar  

<img width="687" height="332" alt="Screenshot 2025-08-29 152455" src="https://github.com/user-attachments/assets/3484457a-3b5d-447e-8fc1-2eb7ec77b588" />

#### 📊 D) Song Longevity Distribution
- **Rows**: `Weeks_in_chart` (grouped into ranges: 1–5, 6–10, 11–20…)  
- **Values**: Count of `Song`  
- Chart: Line Chart  

<img width="694" height="328" alt="Screenshot 2025-08-29 152508" src="https://github.com/user-attachments/assets/cc546f62-25b6-43ec-b611-7fdfde4cf527" />

### 3. Dashboard Design
- Created **Dashboard sheet**:
  - Title: *“Billboard Music Trends Dashboard”*.
  - Added **slicers** for `Year`, `Decade`, `Chart`, `Artist`.
  - Connected slicers to all PivotTables.
  - Arranged charts in a **2x2 grid** for readability.
- Applied consistent formatting, colors, and chart titles.

<img width="195" height="198" alt="Screenshot 2025-08-29 152336" src="https://github.com/user-attachments/assets/0da1785c-9deb-4123-9304-257e2469c1cd" />
<img width="196" height="282" alt="Screenshot 2025-08-29 152351" src="https://github.com/user-attachments/assets/d61a57af-f3f6-49c3-bb89-d475b852409f" />
<img width="198" height="303" alt="Screenshot 2025-08-29 152420" src="https://github.com/user-attachments/assets/4427032d-9bcc-4b51-8ba1-14895843e104" />
<img width="198" height="323" alt="Screenshot 2025-08-29 152402" src="https://github.com/user-attachments/assets/ed96281b-e4d0-4680-a5d3-b99d5ea183cd" />

## 🔢 Helper Columns & Formulas
In Power Query, I added new calculated columns for deeper analysis:

* **Is\_New** → identifies if a song entered the chart for the first time.

  ```m
  = if [last_week] = null then "Yes" else "No"
  ```

* **Rank\_Change** → calculates how many positions the song moved compared to last week.

  ```m
  = if [last_week] = null then null else [last_week] - [rank]
  ```

* **Year** → extracts year from the date.

  ```m
  = Date.Year([date])
  ```

* **Month (MMM-YYYY)** → extracts month in short format + year.

  ```m
  = Date.ToText([date], "MMM-yyyy")
  ```

* **Decade** → groups songs by decade (e.g., 1990s, 2000s).

  ```m
  = Number.ToText(Number.RoundDown(Date.Year([date]) / 10) * 10) & "s"
  ```

* **Week Range** → groups songs by number of weeks they stayed on chart.

  ```m
  = Table.AddColumn(#"Filtered Rows", "Week Range", each 
    if [Weeks in Charts] <= 5 then "1-5"
    else if [Weeks in Charts] <= 10 then "6-10"
    else if [Weeks in Charts] <= 20 then "11-20"
    else if [Weeks in Charts] <= 30 then "21-30"
    else if [Weeks in Charts] <= 40 then "31-40"
    else if [Weeks in Charts] <= 50 then "41-50"
    else if [Weeks in Charts] <= 60 then "51-60"
    else if [Weeks in Charts] <= 70 then "61-70"
    else if [Weeks in Charts] <= 80 then "71-80"
    else if [Weeks in Charts] <= 100 then "81-100"
    else if [Weeks in Charts] <= 150 then "101-150"
    else if [Weeks in Charts] <= 200 then "151-200"
    else if [Weeks in Charts] <= 300 then "201-300"
    else if [Weeks in Charts] <= 500 then "301-500"
    else "501+")
  ```
## ✅ Conclusion

This project demonstrates how **Power Query + Excel** can be used to clean, transform, and analyze large music chart datasets.
By combining multiple Billboard sources, building **calculated columns**, and creating an interactive **dashboard**.
* How songs perform across different chart types 📈

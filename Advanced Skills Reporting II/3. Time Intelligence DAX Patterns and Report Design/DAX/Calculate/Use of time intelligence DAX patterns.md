**Time Intelligence DAX patterns** are a set of predefined calculations that help perform time-based analysis using DAX in Power BI, Power Pivot, and SSAS Tabular. These patterns allow you to analyze data over time, such as calculating year-to-date, quarter-over-quarter growth, moving averages, and comparing current performance to prior periods.

Here are some of the most common **Time Intelligence DAX patterns** and their use cases:

---

### 1. **Year-to-Date (YTD)**
Calculates the cumulative value from the start of the year to a specific date.

#### **DAX Pattern**
```DAX
YTD Sales = 
TOTALYTD(
    [Total Sales], 
    'Date'[Date]
)
```

#### Explanation:
- **`TOTALYTD()`**: Calculates the year-to-date total of the `[Total Sales]` measure, using the date column `'Date'[Date]` to determine the year boundaries.
  
---

### 2. **Month-to-Date (MTD)**
Calculates the cumulative value from the start of the current month to a specific date.

#### **DAX Pattern**
```DAX
MTD Sales = 
TOTALMTD(
    [Total Sales], 
    'Date'[Date]
)
```

#### Explanation:
- **`TOTALMTD()`**: Calculates the month-to-date total of the `[Total Sales]` measure, based on the date column `'Date'[Date]`.

---

### 3. **Quarter-to-Date (QTD)**
Calculates the cumulative value from the start of the current quarter to a specific date.

#### **DAX Pattern**
```DAX
QTD Sales = 
TOTALQTD(
    [Total Sales], 
    'Date'[Date]
)
```

#### Explanation:
- **`TOTALQTD()`**: Calculates the quarter-to-date total of the `[Total Sales]` measure, using the date column `'Date'[Date]`.

---

### 4. **Same Period Last Year (SPLY)**
Calculates the total value for the same period in the previous year.

#### **DAX Pattern**
```DAX
Sales SPLY = 
CALCULATE(
    [Total Sales], 
    SAMEPERIODLASTYEAR('Date'[Date])
)
```

#### Explanation:
- **`SAMEPERIODLASTYEAR()`**: Returns a table of dates for the same period in the previous year.
- **`CALCULATE()`**: Changes the filter context to apply the previous year’s period when calculating `[Total Sales]`.

---

### 5. **Moving Average (Rolling 3-Month Average)**
Calculates a rolling average over a 3-month period.

#### **DAX Pattern**
```DAX
3-Month Moving Average = 
CALCULATE(
    AVERAGEX(
        DATESINPERIOD('Date'[Date], 
        LASTDATE('Date'[Date]), 
        -3, 
        MONTH
    ), 
    [Total Sales]
)
```

#### Explanation:
- **`DATESINPERIOD()`**: Returns a table of dates starting from the last date in the filter context and going back 3 months.
- **`AVERAGEX()`**: Averages the `[Total Sales]` for each date in the 3-month period.
- **`CALCULATE()`**: Changes the filter context for calculating the moving average.

---

### 6. **Year-over-Year Growth (YoY)**
Calculates the percentage growth in sales or any measure compared to the same period in the previous year.

#### **DAX Pattern**
```DAX
YoY Growth = 
DIVIDE(
    [Total Sales] - [Sales SPLY], 
    [Sales SPLY], 
    0
)
```

#### Explanation:
- **`[Total Sales]`**: The sales amount for the current period.
- **`[Sales SPLY]`**: The sales amount for the same period last year (calculated using the `SAMEPERIODLASTYEAR` function).
- **`DIVIDE()`**: Performs division while handling division by zero, calculating the year-over-year growth.

---

### 7. **Month-over-Month Growth (MoM)**
Calculates the percentage growth in sales or any measure compared to the previous month.

#### **DAX Pattern**
```DAX
MoM Growth = 
DIVIDE(
    [Total Sales] - [Sales Previous Month], 
    [Sales Previous Month], 
    0
)

Sales Previous Month = 
CALCULATE(
    [Total Sales], 
    PREVIOUSMONTH('Date'[Date])
)
```

#### Explanation:
- **`PREVIOUSMONTH()`**: Returns a table with the dates of the previous month.
- **`DIVIDE()`**: Performs the month-over-month growth calculation.

---

### 8. **Cumulative Total**
Calculates the running total over time (e.g., cumulative sales).

#### **DAX Pattern**
```DAX
Cumulative Sales = 
CALCULATE(
    [Total Sales], 
    FILTER(
        ALL('Date'[Date]), 
        'Date'[Date] <= MAX('Date'[Date])
    )
)
```

#### Explanation:
- **`ALL()`**: Removes filters on the `'Date'[Date]` column.
- **`FILTER()`**: Filters the dates that are less than or equal to the maximum date in the current context.
- **`CALCULATE()`**: Changes the filter context to calculate the cumulative total.

---

### 9. **Last N Days**
Calculates the total sales over the last N days, for example, the last 30 days.

#### **DAX Pattern**
```DAX
Sales Last 30 Days = 
CALCULATE(
    [Total Sales], 
    DATESINPERIOD(
        'Date'[Date], 
        LASTDATE('Date'[Date]), 
        -30, 
        DAY
    )
)
```

#### Explanation:
- **`DATESINPERIOD()`**: Creates a table with dates for the last 30 days.
- **`CALCULATE()`**: Adjusts the filter context to limit the calculation to the last 30 days.

---

### 10. **First Date and Last Date**
Retrieve the first and last date in a period, such as for showing the range of a time window.

#### **DAX Pattern**
```DAX
First Date = 
FIRSTDATE('Date'[Date])

Last Date = 
LASTDATE('Date'[Date])
```

#### Explanation:
- **`FIRSTDATE()`**: Returns the first date in the current filter context.
- **`LASTDATE()`**: Returns the last date in the current filter context.

---

### 11. **Previous Quarter**
Calculates the total sales for the previous quarter.

#### **DAX Pattern**
```DAX
Sales Previous Quarter = 
CALCULATE(
    [Total Sales], 
    PREVIOUSQUARTER('Date'[Date])
)
```

#### Explanation:
- **`PREVIOUSQUARTER()`**: Returns a table of dates corresponding to the previous quarter.
- **`CALCULATE()`**: Changes the filter context to compute total sales for the previous quarter.

---

### 12. **Parallel Period**
Calculates the value for the same period in another parallel time window (e.g., the same month last year or last quarter).

#### **DAX Pattern**
```DAX
Sales Parallel Period = 
CALCULATE(
    [Total Sales], 
    PARALLELPERIOD('Date'[Date], -1, YEAR)
)
```

#### Explanation:
- **`PARALLELPERIOD()`**: Shifts the time period by a specified number of intervals (e.g., -1 year, -1 month).
- **`CALCULATE()`**: Changes the filter context to apply the shifted period.

---

### 13. **Days Between Two Dates**
Calculates the difference in days between two specific dates.

#### **DAX Pattern**
```DAX
Days Between Dates = 
DATEDIFF('Date'[Start Date], 'Date'[End Date], DAY)
```

#### Explanation:
- **`DATEDIFF()`**: Returns the number of intervals (in this case, days) between the two dates `'Start Date'` and `'End Date'`.

---

### Summary:
These patterns can be used individually or in combination to perform complex time-based calculations in Power BI or other tools using DAX. Time Intelligence is one of the most powerful features in DAX, enabling business users to analyze trends over time and make data-driven decisions.
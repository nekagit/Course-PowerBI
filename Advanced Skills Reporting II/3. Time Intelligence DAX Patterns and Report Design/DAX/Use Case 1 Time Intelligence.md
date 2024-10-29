Here are example tasks for a 1.45 min practice session for **Case Study 1: Use of Time Intelligence DAX Patterns**. These tasks focus on understanding and applying Time Intelligence DAX functions in Power BI.

### Task 1: **Calculate Year-to-Date (YTD) Sales**
- Use the `TOTALYTD()` DAX function to calculate the **year-to-date** sales.
- **Objective**: Identify how the sales trend has progressed since the beginning of the year.

```DAX
YTD_Sales = TOTALYTD(SUM(Sales[Amount]), 'Date'[Date])
```

### Task 2: **Compare Current Year Sales with Previous Year**
- Use the `SAMEPERIODLASTYEAR()` function to calculate sales from the previous year and compare it with current year sales.
- **Objective**: Analyze sales growth or decline year-over-year.

```DAX
Previous_Year_Sales = CALCULATE(SUM(Sales[Amount]), SAMEPERIODLASTYEAR('Date'[Date]))
```

### Task 3: **Calculate Sales Growth over Time**
- Use the `DATESBETWEEN()` function to calculate sales for a specific date range (e.g., last quarter).
- **Objective**: Analyze sales growth for the current period vs. a previous period.

```DAX
Sales_Last_Quarter = CALCULATE(SUM(Sales[Amount]), DATESBETWEEN('Date'[Date], DATE(2023, 7, 1), DATE(2023, 9, 30)))
```

### Task 4: **Calculate Moving Average Sales**
- Use the `DATESINPERIOD()` function to calculate a moving average of sales over the last 30 days.
- **Objective**: Smooth out daily sales data for better trend analysis.

```DAX
Moving_Avg_Sales_30_Days = CALCULATE(AVERAGE(Sales[Amount]), DATESINPERIOD('Date'[Date], LASTDATE('Date'[Date]), -30, DAY))
```

### Task 5: **Calculate Quarter-to-Date (QTD) Sales**
- Use the `TOTALQTD()` function to calculate **quarter-to-date** sales.
- **Objective**: Track the sales performance within the current quarter.

```DAX
QTD_Sales = TOTALQTD(SUM(Sales[Amount]), 'Date'[Date])
```

### Task 6: **Show Monthly Sales Breakdown**
- Use the `MONTH()` and `SUM()` functions to calculate monthly sales totals for the current year.
- **Objective**: Break down sales data by month for a detailed view of performance.

```DAX
Monthly_Sales = CALCULATE(SUM(Sales[Amount]), MONTH('Date'[Date]) = MONTH(TODAY()))
```

### Task 7: **Create a Year-over-Year Sales Growth Measure**
- Use the `DIVIDE()` and `SAMEPERIODLASTYEAR()` functions to calculate year-over-year growth percentage.
- **Objective**: Understand the percentage change in sales compared to the previous year.

```DAX
YOY_Sales_Growth = DIVIDE([Current_Year_Sales] - [Previous_Year_Sales], [Previous_Year_Sales], 0)
```

### Task 8: **Calculate Last 12 Months (LTM) Sales**
- Use the `DATESINPERIOD()` function to calculate **last 12 months** sales totals.
- **Objective**: Track rolling 12-month sales performance.

```DAX
LTM_Sales = CALCULATE(SUM(Sales[Amount]), DATESINPERIOD('Date'[Date], LASTDATE('Date'[Date]), -12, MONTH))
```


### Task 09: **Track Sales Trend Over Multiple Periods**
- Use `PARALLELPERIOD()` to track sales performance over the last few months.
- **Objective**: Compare sales trends for different months within the same year.

```DAX
Sales_Last_Month = CALCULATE(SUM(Sales[Amount]), PARALLELPERIOD('Date'[Date], -1, MONTH))
```

These tasks cover a range of Time Intelligence DAX patterns and should fit within a practice session of 1.45 minutes.
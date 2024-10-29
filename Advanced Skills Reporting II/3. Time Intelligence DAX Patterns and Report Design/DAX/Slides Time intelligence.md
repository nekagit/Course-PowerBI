Here’s a list of bullet points for a 10-slide presentation on **Time Intelligence DAX Patterns**:

### Slide 1: **Introduction to Time Intelligence in DAX**
- **Definition**: Time intelligence refers to calculations related to dates, periods, and times.
- DAX provides built-in time intelligence functions to analyze data over time.
- Essential for comparing periods, year-to-date calculations, and cumulative totals.

### Slide 2: **Importance of Time Intelligence**
- Allows users to track trends, seasonal patterns, and business performance over time.
- Vital for financial reporting, sales analysis, and forecasting.
- Supports data-driven decision-making with a time-based context.

### Slide 3: **Basic Time Intelligence Functions**
- **DATEADD**: Shifts a date by a specified interval (e.g., days, months, years).
- **SAMEPERIODLASTYEAR**: Returns the corresponding period in the previous year.
- **DATESYTD**: Calculates year-to-date totals from the beginning of the year until the selected date.

### Slide 4: **Year-to-Date (YTD) Patterns**
- **TOTALYTD**: Aggregates values from the start of the year to the specified date.
- Common use cases: calculating cumulative sales, expenses, or profits.
- **Example**: `TOTALYTD(SUM(Sales[Amount]), Dates[Date])`

### Slide 5: **Quarter-to-Date (QTD) and Month-to-Date (MTD) Patterns**
- **TOTALQTD**: Calculates the cumulative total from the start of the quarter to the selected date.
- **TOTALMTD**: Calculates cumulative total from the start of the month to the selected date.
- Used for comparing performance over quarters and months.

### Slide 6: **Rolling and Moving Averages**
- **Moving Averages**: Smooths out trends by averaging values over rolling time periods.
- Example patterns: 30-day moving average, 3-month rolling average.
- **Example**: `AVERAGEX(DATESINPERIOD(Dates[Date], MAX(Dates[Date]), -30, DAY), [Sales])`

### Slide 7: **Comparing Periods**
- **SAMEPERIODLASTYEAR**: Compares performance with the same period in the previous year.
- **PARALLELPERIOD**: Returns a parallel period from a different year, quarter, or month.
- **Example**: Analyze sales growth by comparing current year to previous year.

### Slide 8: **Custom Time Period Calculations**
- **DATEADD**: Flexible function to calculate for custom time ranges (e.g., last 12 months).
- **DATESBETWEEN**: Allows specifying a custom date range for comparisons or aggregations.
- Useful for comparing non-standard periods (e.g., fiscal years).

### Slide 9: **Cumulative Totals and Running Totals**
- **Running Totals**: Accumulate values over time, typically used in sales and financial reporting.
- **Example**: `CALCULATE(SUM(Sales[Amount]), FILTER(ALL(Dates), Dates[Date] <= MAX(Dates[Date])))`
- Shows the cumulative progress over days, months, or years.

### Slide 10: **Best Practices for Time Intelligence**
- Ensure proper date table with contiguous dates for DAX functions to work correctly.
- Use `CALCULATE` to manipulate filter context for more control over time-based calculations.
- Test different patterns (e.g., YTD, rolling totals) to match business needs.
- Combine time intelligence functions with other DAX expressions for advanced analysis.
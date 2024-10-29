### Define the measure for Total Annual Profit

```dax
DEFINE
    MEASURE financials[TotalAnnualProfit] = CALCULATE(SUM(financials[Profit]))
```

### Get the top 10 rows based on Profit

```dax
EVALUATE
    TOPN(
        10,
        financials,
        [TotalAnnualProfit], DESC
    )
```

### Calculate Total Annual Profit

```dax
EVALUATE
    ROW(
        "TotalAnnualProfit", 
        CALCULATE(SUM(financials[Profit]))
    )
```

### Calculate Total Negative Profit

```dax
EVALUATE
    ROW(
        "TotalNegativeProfit", 
        CALCULATE(
            SUMX(
                FILTER(
                    financials,
                    financials[Profit] < 0
                ),
                financials[Profit]
            )
        )
    )
```

### Calculate Total Annual Profit, Total Positive Profit, and Total Negative Profit in One Table

```dax
DEFINE
    MEASURE financials[TotalAnnualProfit] = CALCULATE(SUM(financials[Profit]))

EVALUATE
    ROW(
        "TotalAnnualProfit", 
        [TotalAnnualProfit],
        "TotalPositiveProfit",
        CALCULATE(
            SUMX(
                FILTER(
                    financials,
                    financials[Profit] > 0
                ),
                financials[Profit]
            )
        ),
        "TotalNegativeProfit",
        CALCULATE(
            SUMX(
                FILTER(
                    financials,
                    financials[Profit] < 0
                ),
                financials[Profit]
            )
        )
    )
```

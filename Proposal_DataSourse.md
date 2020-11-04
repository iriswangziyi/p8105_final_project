Proposal\_DataSource
================
Wenbo Fei
11/3/2020

# Data 1

Aggregated yearly beer statistics by state from 2008-2019[Beer Statistic
– Aggregated data: Tax Determined (in
Barrels)](https://www.ttb.gov/beer/statistics)

``` r
#install.packages("gdata")
site1 <- "http://www.ttb.gov/images/pdfs/statistics/aggregated/aggr-data-beer_2008-2019.xlsx"
data1  <- 
  gdata::read.xls(site1, header = T, skip = 6, nrow = 52)
#View(data1)
```

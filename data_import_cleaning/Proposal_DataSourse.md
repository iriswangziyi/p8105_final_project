Proposal\_DataSource
================
Wenbo Fei
11/3/2020

# Data 1 Tax data of beer

Yearly Statistical Beer Data by State (2008 – 2019) from [Alcohol and
Tobacco Tax and Trade Bureau](https://www.ttb.gov/beer/statistics). This
aggregated data contained records on Tax Determined, Taxable Volume of
Bottles and Cans, Taxable Volume of Barrels and Kegs each year for each
state in barrels.

``` r
#install.packages("gdata")
site1 = "http://www.ttb.gov/images/pdfs/statistics/aggregated/aggr-data-beer_2008-2019.xlsx"

#Tax Determined (in Barrels)
tax_df  =  
  gdata::read.xls(site1, sheet = 1, header = T, skip = 6, nrow = 52) %>% 
  janitor::clean_names()

# Taxable Volume of Bottles and Cans* (in Barrels)
taxable_cans_df  = 
  gdata::read.xls(site1, sheet = 2, header = T, skip = 4, nrow = 52) %>% 
  janitor::clean_names()

# Taxable Volume of Barrels and Kegs*
taxable_barrels_df  = 
  gdata::read.xls(site1, sheet = 3, header = T, skip = 4, nrow = 52) %>%
  janitor::clean_names()


#View(tax_df)
#View(taxable_cans_df)
#View(taxable_barrels_df)
```

## Data 2: Beer Product Information

Open Beer database from
[Opendatasoft](https://data.opendatasoft.com/explore/dataset/open-beer-database%40public-us/information/?rows=4588&timezone=&refine.country=United+States&location=2,16.98232,9.498&basemap=jawg.sunny&dataChart=eyJxdWVyaWVzIjpbeyJjb25maWciOnsiZGF0YXNldCI6Im9wZW4tYmVlci1kYXRhYmFzZUBwdWJsaWMtdXMiLCJvcHRpb25zIjp7fX0sImNoYXJ0cyI6W3siYWxpZ25Nb250aCI6dHJ1ZSwidHlwZSI6ImxpbmUiLCJmdW5jIjoiQVZHIiwieUF4aXMiOiJhYnYiLCJzY2llbnRpZmljRGlzcGxheSI6dHJ1ZSwiY29sb3IiOiIjMTQyRTdCIn1dLCJ4QXhpcyI6Imxhc3RfbW9kIiwibWF4cG9pbnRzIjoiIiwidGltZXNjYWxlIjoieWVhciIsInNvcnQiOiIifV0sImRpc3BsYXlMZWdlbmQiOnRydWUsImFsaWduTW9udGgiOnRydWV9).
This dataset contains information of each beer product, including
product name, universal product code, style, category, brewer along with
its address and website, percentage of alcohol by volume, bitterness
from hops in a beer, beer color, and description in text.

``` r
beer_specific = 
  read_delim("https://public-us.opendatasoft.com/explore/dataset/open-beer-database/download/?format=csv&timezone=America/New_York&lang=en&use_labels_for_header=true&csv_separator=%3B", delim = ";") %>%
  janitor::clean_names()
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   cat_id = col_double(),
    ##   `Alcohol By Volume` = col_double(),
    ##   `International Bitterness Units` = col_double(),
    ##   `Standard Reference Method` = col_double(),
    ##   `Universal Product Code` = col_double(),
    ##   last_mod = col_datetime(format = "")
    ## )

    ## See spec(...) for full column specifications.

    ## Warning: 1 parsing failure.
    ##  row    col               expected          actual                                                                                                                                                                        file
    ## 3565 cat_id no trailing characters /22/10 08:00 PM 'https://public-us.opendatasoft.com/explore/dataset/open-beer-database/download/?format=csv&timezone=America/New_York&lang=en&use_labels_for_header=true&csv_separator=%3B'

``` r
#View(beer_specific)
```

  - This dataset seems to have many missing values. Some of them don’t
    have a description, many of them share a product code 0.
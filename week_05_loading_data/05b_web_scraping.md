Web Scraping
========================================================
author: Bob Horton
date: 2015-02-23

Read HTML Table
========================================================

```r
site <- "http://en.wikipedia.org/wiki/List_of_countries_by_life_expectancy"
mydf <- XML::readHTMLTable(site, which=3, stringsAsFactors=F)
kable(head(mydf))
```



|Rank |state/territory    |Overall |Male  |Female |
|:----|:------------------|:-------|:-----|:------|
|1    |Japan              |82.73   |79.29 |86.96  |
|2    |Switzerland        |81.81   |79.31 |84.12  |
|3    |Hong Kong ( China) |81.61   |79.04 |84.30  |
|4    |Australia          |81.44   |79.12 |84     |
|5    |Italy              |81.37   |78.58 |83.98  |
|6    |Iceland            |81.28   |79.49 |83.05  |

rvest
========================================================
(ha)rvest data from the web.

magrittr
========================================================

![Ceci n'est pas un pipe](http://upload.wikimedia.org/wikipedia/en/b/b9/MagrittePipe.jpg)

***

[%>%](http://cran.r-project.org/web/packages/magrittr/vignettes/magrittr.html)

selectorGadget
========================================================

Allows you to interactively click on parts of a web page and use a process of positive nad negative seletcion to generate CSS selectors for targeted information.

rvest
========================================================


```r
# devtools::install_github("hadley/rvest")
library(magrittr)
library(rvest)
cigcancerpage <- html("http://lib.stat.cmu.edu/DASL/Datafiles/cigcancerdat.html")
txt_con <- cigcancerpage %>% 
  html_nodes("pre") %>% .[2] %>% 
  html_text() %>% textConnection()
headers <- readLines(txt_con,2) %>% .[2] %>% 
  gsub("^\\s+", "", .) %>%
  strsplit("\\s+") %>% .[[1]]
cigcancer <- read.delim(txt_con, header=F)
colnames(cigcancer) <- headers
```

rvest
========================================================


|STATE |   CIG| BLAD|  LUNG|  KID| LEUK|
|:-----|-----:|----:|-----:|----:|----:|
|AL    | 18.20| 2.90| 17.05| 1.59| 6.15|
|AZ    | 25.82| 3.52| 19.80| 2.75| 6.61|
|AR    | 18.24| 2.99| 15.98| 2.02| 6.94|
|CA    | 28.60| 4.46| 22.07| 2.66| 7.06|
|CT    | 31.10| 5.11| 22.83| 3.35| 7.20|
|DE    | 33.60| 4.78| 24.55| 3.36| 6.45|

[Cigarette Cancer Data](http://lib.stat.cmu.edu/DASL/Datafiles/cigcancerdat.html)

Interesting Tables in Wikipedia
========================================================

http://en.wikipedia.org/wiki/List_of_cancer_mortality_rates_in_the_United_States
http://en.wikipedia.org/wiki/List_of_countries_by_cancer_rate
http://en.wikipedia.org/wiki/Prevalence_of_tobacco_consumption
http://stats.wikimedia.org/EN/TablesWikipediaEN.htm

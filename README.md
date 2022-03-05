# Naknade saborskih zastupnika
Uređeni podaci o zastupničkim naknadama (od 2012. godine, tj. početka 7. saziva). Napravljeno u sklopu [ODD-a 2022](http://odd.codeforcroatia.org/konferencija/).

> **Izvor podataka**: [Arhiva](https://www.sabor.hr/hr/press/javnost-rada/arhiva) Sabora 
> 
> **Datum pristupanja**: 05.03.2022.
> 
> **Autor**: Filip Rodik

Podaci o zastupničkim naknadama spojeni su s podacima o zastupnicima pojedinog saziva gdje je navedena i stranačka pripadnost zastupnika/ce.
## 


Primjer `R` skripte za učitavanje i analizu podataka:
``` r
library(readr)
library(tidyverse)
library(lubridate)

# path to zastupnicke_naknade.csv
file_name <- "path/to/file/zastupnicke_naknade.csv"

# locale for csv reading
loc <- locale(
    "hr",
    decimal_mark = ",",
    grouping_mark = ".",
    tz = "UTC",
    encoding = "UTF-8",
    asciify = FALSE
)

# read csv
raw_data <- read_delim(
    file_name, 
    quote = "", 
    delim = ";",
    locale = loc
) 

# fix data types
naknade <- raw_data %>% mutate(
    Od = dmy(Od),
    Do = dmy(Do),
    Ukupno = as.double(Ukupno)
)

# analyse
naknade %>% 
    group_by(Godina, Stranka) %>% 
    summarise(Total = sum(Ukupno), .groups = 'drop') %>% 
    arrange(desc(Total)) %>% 
    pivot_wider(names_from = Godina, values_from = Total, names_sort = TRUE) %>% 
``` 

|Stranka                           |       2012|       2013|       2014|       2015|       2016|       2017|       2018|       2019|       2020|       2021|
|:---------------------------------|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|----------:|
|SDP                               | 3416592.80| 3628454.98| 3904088.68| 3511019.84| 1660442.43| 1720836.85| 1737254.32| 1675747.91|  831301.91|  709821.06|
|HDZ                               | 1967376.06| 2309888.12| 2325981.81| 2003366.94| 2412937.05| 3485318.21| 3728200.65| 3653970.30| 2355146.45| 3297660.78|
|NZ                                |  295892.85|  365726.26|  446148.58|  421263.73|  467959.30|  754315.92|  870020.71|  820631.16|  707914.67| 1200613.50|
|HNS                               |  700380.49|  875843.09|  823526.84|  783679.14|  217033.87|  193451.39|  242889.85|  236160.36|  101045.33|   26559.00|
|Most                              |         NA|         NA|         NA|         NA|  676180.22|  734657.41|  521490.18|  546758.44|  410792.81|  373478.32|
|HDSSB                             |  548635.31|  537324.24|  566408.95|  495333.03|  119040.06|   80123.87|   89359.11|   80893.40|   38000.43|         NA|
|HSU                               |  203348.23|  250537.77|  330389.17|  299719.57|  153639.49|  173174.13|  173988.68|  170176.74|  101399.68|   99094.65|
|NLM                               |         NA|         NA|         NA|         NA|   22047.60|  139191.08|  238540.35|  267233.30|  122745.39|         NA|
|HSS                               |   12656.00|   22040.00|   22580.00|   18160.00|   77182.52|  201970.16|  254082.12|  255924.69|  134201.92|   58966.65|
|IDS                               |  152995.87|  168581.30|  162989.77|  158617.11|  100460.65|  167216.47|  169718.35|  247746.83|  204872.13|  246796.90|
|Reformisti                        |  174102.64|  169312.88|  204271.20|  243665.41|   40856.19|       0.00|       0.00|       0.00|    4875.00|   31771.94|
|Hrvatski laburisti - Stranka rada |  150092.09|  175021.53|  205599.82|  138743.04|         NA|         NA|         NA|         NA|         NA|         NA|
|Domovinski pokret                 |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|   50574.79|  202252.78|
|SDSS                              |  192523.01|  169860.12|  169118.20|  166240.83|   65989.19|  105615.25|   91051.02|   99400.86|  121458.99|  190872.72|
|N/A                               |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|   72199.89|  176751.90|
|Hrvatski suverenisti              |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|   50627.88|  168880.07|
|GLAS                              |         NA|         NA|         NA|         NA|   20845.21|  133553.78|  144659.43|  156168.53|   34307.83|       0.00|
|ORaH                              |  129541.01|  142132.29|  149361.86|  127560.59|         NA|         NA|         NA|         NA|         NA|         NA|
|HSP AS                            |         NA|         NA|         NA|         NA|  123944.86|         NA|         NA|         NA|         NA|         NA|
|Novi val                          |  104718.43|  103189.13|  115440.93|   96634.30|         NA|         NA|         NA|         NA|         NA|         NA|
|BM 365                            |         NA|         NA|         NA|         NA|   21978.06|  106560.48|  113056.34|  107929.23|   53218.97|         NA|
|HDS                               |         NA|         NA|         NA|         NA|   66515.00|  103136.10|  104966.63|   94617.13|   60567.45|   42642.00|
|HRAST                             |         NA|         NA|         NA|         NA|   66221.38|  100452.62|   99708.53|   98844.25|   48554.34|         NA|
|HSP dr. Ante Starčević            |   77228.93|   79515.12|   98583.36|   81053.00|         NA|         NA|         NA|         NA|         NA|         NA|
|ID                                |   81507.31|   81066.65|   84806.52|   82711.61|         NA|         NA|         NA|         NA|         NA|         NA|
|Živi zid                          |         NA|         NA|         NA|         NA|    5721.81|   75862.00|   59723.57|   43175.22|   12500.00|         NA|
|HGS                               |   75025.74|   74599.08|   70146.44|   64386.94|         NA|         NA|         NA|         NA|         NA|         NA|
|BDSH                              |   64858.41|   72555.14|   72346.02|   66338.98|         NA|         NA|         NA|         NA|         NA|         NA|
|Hrvatski laburisti                |         NA|         NA|         NA|         NA|   51947.23|         NA|         NA|         NA|         NA|         NA|
|Centar                            |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|    4668.83|   44730.75|
|Naprijed Hrvatska!                |   24775.94|   28815.50|   30248.08|   11154.27|         NA|         NA|         NA|         NA|         NA|         NA|
|PH                                |         NA|         NA|         NA|         NA|   28261.00|       0.00|       0.00|       0.00|       0.00|         NA|
|NLSP                              |         NA|         NA|         NA|         NA|   14020.64|         NA|         NA|         NA|         NA|         NA|
|HSLS                              |         NA|         NA|         NA|         NA|   12940.00|       0.00|       0.00|       0.00|    5403.78|    9741.22|
|Blok                              |         NA|         NA|         NA|         NA|    2700.00|    3296.36|    8308.75|    2107.25|       0.00|       0.00|
|Demokrati                         |         NA|         NA|         NA|         NA|       0.00|    6280.26|       0.00|       0.00|       0.00|         NA|
|NHR                               |         NA|         NA|         NA|         NA|    3975.00|       0.00|    3326.00|       0.00|       0.00|         NA|
|Damir Bajs NL                     |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|    1760.00|
|Možemo!                           |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|       0.00|    1088.69|
|DC                                |         NA|         NA|       0.00|       0.00|         NA|         NA|         NA|         NA|         NA|         NA|
|BUZ                               |         NA|         NA|         NA|         NA|       0.00|         NA|         NA|         NA|         NA|         NA|
|HRID                              |         NA|         NA|         NA|         NA|       0.00|         NA|         NA|         NA|         NA|         NA|
|SIP                               |         NA|         NA|         NA|         NA|       0.00|       0.00|       0.00|       0.00|       0.00|         NA|
|SNAGA                             |         NA|         NA|         NA|         NA|       0.00|       0.00|       0.00|       0.00|       0.00|         NA|
|Fokus                             |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|       0.00|       0.00|
|NL                                |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|       0.00|       0.00|
|RF                                |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|       0.00|       0.00|
|SsIP                              |         NA|         NA|         NA|         NA|         NA|         NA|         NA|         NA|       0.00|       0.00|

# Napomene
Podaci za 2016. godinu i ranije dobiveni su OCR-anjem PDF datoteka. Osim toga, dio obrade podataka rađen je ručno u Excelu. Ukoliko uočite greške u podacima možete:
- otvoriti Issue u ovom repozitoriju s opisom problema
- napraviti Pull request s ispravljenom verzijom CSV-a

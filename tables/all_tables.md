# Paper A: Tables

## Table 1: Dataset Overview

```
     Dataset      Year Vehicles Countries Manufacturers Models Energy_Available
1 OBFCM 2021      2021   109327        29            23    271           108090
2 OBFCM 2022      2022   156276        29            26    372           152153
3 OBFCM 2023      2023        0         0             0      0                0
4      Total 2021-2023   265603        29            30    485           260243
  EDS_Available
1        109327
2        156276
3             0
4        265603
```

## Table 2: Summary Statistics

```
                         Variable      N    Mean  Median     SD     Min     Q25
25%...1 Total Energy [kWh/100 km] 260243   22.60   21.65   5.80    0.41   18.97
25%...2                   EDS [%] 265603   30.54   28.14  20.36    0.00   13.63
25%...3                 Mass [kg] 264824 2100.49 2020.00 270.53 1672.00 1926.00
25%...4                  AER [km] 260514   61.20   59.00  19.51   13.00   50.00
            Q75     Max
25%...1   25.22  125.11
25%...2   44.72   99.46
25%...3 2245.00 3086.00
25%...4   69.00  427.00
```

## Table 3: Variable Importance (LMG)

```
# A tibble: 3 × 3
  Variable       LMG_Contribution CI_95   
  <chr>                     <dbl> <chr>   
1 mass                      97.5  [NA, NA]
2 aer                        1.41 [NA, NA]
3 region_numeric             1.08 [NA, NA]
```

## Table 4: Fleet vs Campaign Comparison

```
# A tibble: 1 × 7
  Dataset       Energy_Mean Energy_Median Energy_SD EDS_Mean EDS_Median EDS_SD
  <chr>               <dbl>         <dbl>     <dbl>    <dbl>      <dbl>  <dbl>
1 Fleet (OBFCM)        22.6          21.6       5.8     30.5       28.1   20.4
```


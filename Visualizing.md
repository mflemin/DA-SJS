Visualizing Project
================
Matt Fleming
9/16/20

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
avocado <- read_csv("avocado.csv")
```

    ## Warning: Missing column names filled in: 'X1' [1]

    ## Parsed with column specification:
    ## cols(
    ##   X1 = col_double(),
    ##   Date = col_date(format = ""),
    ##   AveragePrice = col_double(),
    ##   `Total Volume` = col_double(),
    ##   `4046` = col_double(),
    ##   `4225` = col_double(),
    ##   `4770` = col_double(),
    ##   `Total Bags` = col_double(),
    ##   `Small Bags` = col_double(),
    ##   `Large Bags` = col_double(),
    ##   `XLarge Bags` = col_double(),
    ##   type = col_character(),
    ##   year = col_double(),
    ##   region = col_character()
    ## )

# Data Visualization Project

### Scatter Plot: Title

``` r
ggplot(data = avocado, mapping = aes(x = Date, y = AveragePrice, color = type)) + geom_point(alpha = .2) + labs(x = "Date", y = "Price of one Avocado", title = "Trend in Avocado Price over Time", subtitle = "2015-2018", caption = "Source: avocado")
```

![](Visualizing_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Insight:

##### This scatterplot demonstrates the trend in the price for a single avocado between 2015 and 2018. Although there are many outliers in this dataset, the transparency makes it easier to see that the majority of observations follow a specific trend that fluctuates between high and low avocado prices. There are three clear peaks and four distinct minimums, and since the observations begin Jan 2015 with relatively low prices, we can assume that the winter season yields low avocado prices and the summer season yields higher avocado prices. It is also important to note that produce prices generally vary from region to region, which is why there are so many outliers. Additionally, the color aesthetic reveals a clear trend in organic avocados being more expensive, with roughly the entire top half of the plot being one color and the other half being another color.

### Bar Plot: Title

``` r
mushrooms <- read_csv("mushrooms.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_character(),
    ##   bruises = col_logical(),
    ##   `gill-attachment` = col_logical()
    ## )

    ## See spec(...) for full column specifications.

    ## Warning: 210 parsing failures.
    ##  row             col           expected actual            file
    ## 6039 gill-attachment 1/0/T/F/TRUE/FALSE      a 'mushrooms.csv'
    ## 6041 gill-attachment 1/0/T/F/TRUE/FALSE      a 'mushrooms.csv'
    ## 6376 gill-attachment 1/0/T/F/TRUE/FALSE      a 'mushrooms.csv'
    ## 6425 gill-attachment 1/0/T/F/TRUE/FALSE      a 'mushrooms.csv'
    ## 6435 gill-attachment 1/0/T/F/TRUE/FALSE      a 'mushrooms.csv'
    ## .... ............... .................. ...... ...............
    ## See problems(...) for more details.

``` r
mushrooms <- mushrooms %>% rename(sporeprintcolor = `spore-print-color`)
```

``` r
ggplot(data = mushrooms) + geom_bar(mapping = aes(x = sporeprintcolor, fill = class), position = "fill") + labs(x = "Spore Print Color", y = "Relative Frequency", title = "Relative Frequency of Poisonous Mushrooms Based on Spore Color", subtitle = "Buff, Chocolate, Black, Brown, Orange, Green, Purple, White, Yellow", caption = "Source: mushrooms")
```

![](Visualizing_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

### Insight:

##### This bar plot displays the relative frequency of poisonous mushrooms dependent on the color of the mushrooms’ spores. I tried doing this plot with every variable in this dataset and none of them showed any correlation with whether the type of mushroom was poisonous. However, when divided by spore color, it becomes clear that spore color is the determining factor in whether mushrooms are poisonous or edible, as every color is at least 75% poisonous or edible. This plot also tells us that in general, the overwhelming majority of mushrooms are edible. Additionally, although mushrooms with chocolate, green, and white spore colors tend to be primarily poisonous, there is not a certain group of colors that suggest poison mushrooms (i.e. light or dark colors).

``` r
avocado
```

    ## # A tibble: 18,249 x 14
    ##       X1 Date       AveragePrice `Total Volume` `4046` `4225` `4770`
    ##    <dbl> <date>            <dbl>          <dbl>  <dbl>  <dbl>  <dbl>
    ##  1     0 2015-12-27         1.33         64237.  1037. 5.45e4   48.2
    ##  2     1 2015-12-20         1.35         54877.   674. 4.46e4   58.3
    ##  3     2 2015-12-13         0.93        118220.   795. 1.09e5  130. 
    ##  4     3 2015-12-06         1.08         78992.  1132  7.20e4   72.6
    ##  5     4 2015-11-29         1.28         51040.   941. 4.38e4   75.8
    ##  6     5 2015-11-22         1.26         55980.  1184. 4.81e4   43.6
    ##  7     6 2015-11-15         0.99         83454.  1369. 7.37e4   93.3
    ##  8     7 2015-11-08         0.98        109428.   704. 1.02e5   80  
    ##  9     8 2015-11-01         1.02         99811.  1022. 8.73e4   85.3
    ## 10     9 2015-10-25         1.07         74339.   842. 6.48e4  113  
    ## # … with 18,239 more rows, and 7 more variables: `Total Bags` <dbl>, `Small
    ## #   Bags` <dbl>, `Large Bags` <dbl>, `XLarge Bags` <dbl>, type <chr>,
    ## #   year <dbl>, region <chr>

``` r
mushrooms
```

    ## # A tibble: 8,124 x 23
    ##    class `cap-shape` `cap-surface` `cap-color` bruises odor  `gill-attachmen…
    ##    <chr> <chr>       <chr>         <chr>       <lgl>   <chr> <lgl>           
    ##  1 p     x           s             n           TRUE    p     FALSE           
    ##  2 e     x           s             y           TRUE    a     FALSE           
    ##  3 e     b           s             w           TRUE    l     FALSE           
    ##  4 p     x           y             w           TRUE    p     FALSE           
    ##  5 e     x           s             g           FALSE   n     FALSE           
    ##  6 e     x           y             y           TRUE    a     FALSE           
    ##  7 e     b           s             w           TRUE    a     FALSE           
    ##  8 e     b           y             w           TRUE    l     FALSE           
    ##  9 p     x           y             w           TRUE    p     FALSE           
    ## 10 e     b           s             y           TRUE    a     FALSE           
    ## # … with 8,114 more rows, and 16 more variables: `gill-spacing` <chr>,
    ## #   `gill-size` <chr>, `gill-color` <chr>, `stalk-shape` <chr>,
    ## #   `stalk-root` <chr>, `stalk-surface-above-ring` <chr>,
    ## #   `stalk-surface-below-ring` <chr>, `stalk-color-above-ring` <chr>,
    ## #   `stalk-color-below-ring` <chr>, `veil-type` <chr>, `veil-color` <chr>,
    ## #   `ring-number` <chr>, `ring-type` <chr>, sporeprintcolor <chr>,
    ## #   population <chr>, habitat <chr>

``` r
library(tidyverse)
```

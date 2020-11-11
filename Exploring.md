Exploring
================
Matt Fleming
10/30/20

Load the necessary libraries

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
listings <- read_csv("listings.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   id = col_double(),
    ##   name = col_character(),
    ##   host_id = col_double(),
    ##   host_name = col_character(),
    ##   neighbourhood_group = col_character(),
    ##   neighbourhood = col_character(),
    ##   latitude = col_double(),
    ##   longitude = col_double(),
    ##   room_type = col_character(),
    ##   price = col_double(),
    ##   minimum_nights = col_double(),
    ##   number_of_reviews = col_double(),
    ##   last_review = col_date(format = ""),
    ##   reviews_per_month = col_double(),
    ##   calculated_host_listings_count = col_double(),
    ##   availability_365 = col_double()
    ## )

Take a look inside your dataset

``` r
listings
```

    ## # A tibble: 31,536 x 16
    ##       id name  host_id host_name neighbourhood_g… neighbourhood latitude
    ##    <dbl> <chr>   <dbl> <chr>     <chr>            <chr>            <dbl>
    ##  1   109 Amaz…     521 Paolo     Other Cities     Culver City       34.0
    ##  2   344 Fami…     767 Melissa   Other Cities     Burbank           34.2
    ##  3  2708 Beau…    3008 Chas.     City of Los Ang… Hollywood         34.1
    ##  4  2732 Zen …    3041 Yoga Pri… Other Cities     Santa Monica      34.0
    ##  5  2864 * Be…    3207 Bernadine Other Cities     Bellflower        33.9
    ##  6  5728 Tiny…    9171 Sanni     City of Los Ang… Del Rey           34.0
    ##  7  5729 Zen …    9171 Sanni     City of Los Ang… Del Rey           34.0
    ##  8  5843 Arti…    9171 Sanni     City of Los Ang… Del Rey           34.0
    ##  9  6931 Beau…    3008 Chas.     City of Los Ang… Hollywood         34.1
    ## 10  7874 2nd …   21700 Henry     Other Cities     Bellflower        33.9
    ## # … with 31,526 more rows, and 9 more variables: longitude <dbl>,
    ## #   room_type <chr>, price <dbl>, minimum_nights <dbl>,
    ## #   number_of_reviews <dbl>, last_review <date>, reviews_per_month <dbl>,
    ## #   calculated_host_listings_count <dbl>, availability_365 <dbl>

### Part I: Variation

Perform an analysis of the variation in the “neighbourhood” column.

``` r
ggplot(listings, aes(x = neighbourhood)) +
  geom_bar() + coord_flip()
```

![](Exploring_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
count(listings, neighbourhood) %>%
  arrange(desc(n))
```

    ## # A tibble: 263 x 2
    ##    neighbourhood       n
    ##    <chr>           <int>
    ##  1 Long Beach       1584
    ##  2 Venice           1571
    ##  3 Hollywood        1525
    ##  4 Santa Monica     1139
    ##  5 Downtown         1110
    ##  6 Hollywood Hills   721
    ##  7 West Hollywood    618
    ##  8 Glendale          560
    ##  9 Rowland Heights   521
    ## 10 Beverly Hills     511
    ## # … with 253 more rows

  - Which values are the most common? Why?

> Long Beach is the most common neighborhood because it is a large and
> very popular area, so there are a lot of listings. Since it is not the
> most expensive neighborhood in the area, people whose wealth increased
> recently are either moving into nicer neighborhoods or coming to Long
> Beach from less expensive neighborhoods, so there are a lot of
> properties being bought/sold.

  - Which values are rare? Why? Does that match your expectations?

> There are 55 neighborhoods with less than ten listings, which makes
> sense because LA encompasses a large number of suburbs, so a lot of
> these smaller suburbs don’t have many listings.

  - Can you see any unusual patterns? What might explain them?

> I don’t see any unusual patterns here, other than the fact that there
> are so many neighborhoods in LA.

Perform an analysis of the variation in the “room\_type” column.

``` r
ggplot(listings, aes(x = room_type)) +
  geom_bar()
```

![](Exploring_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

  - Which values are the most common? Why?

> Entire homes/apartments are by far the most common because most people
> looking at real estate listings want to buy their own home.

  - Which values are rare? Why? Does that match your expectations?

> Hotel rooms. This makes sense because not many people are looking to
> rent/buy a hotel room.

  - Can you see any unusual patterns? What might explain them?

> There aren’t really any unusual patterns but the private room had more
> listings than I expected. I guess there are a lot of people that move
> to LA and can’t afford a home and are willing to share an
> apartment/house as long as they get their own room.

Perform an analysis of the variation in the “price” column. Make sure to
explore different “binwidth” values in your analysis.

``` r
ggplot(listings) +
  geom_histogram(aes(x = price), binwidth = 10)
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = price), binwidth = 50)
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-2.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = price), binwidth = 100)
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-3.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = price), binwidth = 10) +
  coord_cartesian(xlim = c(0, 1000))
```

![](Exploring_files/figure-gfm/unnamed-chunk-6-4.png)<!-- -->

  - Which values are the most common? Why?

> Looking at the last graph, which is zoomed in, we can see that the
> most popular listings are at around $100 a night, with the numbers
> significantly dropping off at around $200 a night.

  - Which values are rare? Why? Does that match your expectations?

> The more expensive listings are rare, which matches my expectations
> because people don’t want to pay a ridiculus amount for an Airbnb.
> Also, listings decreasing from $100 are increasingly rare. It is
> probably hard to find a reputable Airbnb for less than around $100.

  - Can you see any unusual patterns? What might explain them?

> It seems that on more appealing numbers, like $100, $250, $500, etc.,
> there is an increase in listings, which is most likely explained
> because people would be willing to pay $500 as opposed to $495, for
> example.

Perform an analysis of the variation in the “minimum\_nights” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(listings) +
  geom_histogram(aes(x = minimum_nights), binwidth = 1)
```

![](Exploring_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = minimum_nights), binwidth = 10)
```

![](Exploring_files/figure-gfm/unnamed-chunk-7-2.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = minimum_nights), binwidth = 50)
```

![](Exploring_files/figure-gfm/unnamed-chunk-7-3.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = minimum_nights), binwidth = 1) +
  coord_cartesian(xlim = c(0,100))
```

![](Exploring_files/figure-gfm/unnamed-chunk-7-4.png)<!-- -->

  - Which values are the most common? Why?

> The most common values occur at \[0,5\] and \~30. It seems like for
> short term stays, most people have the minimum nights set between 1
> and 5, but for longer term stays, a month is a pretty common.

  - Which values are rare? Why? Does that match your expectations?

> Values in between about 5 and 30 (and above 30) are pretty rare, which
> makes sense because most people are either on a brief vacation, and
> only want a listing for a few nights, or need to stay in LA for a
> longer period of time.

  - Can you see any unusual patterns? What might explain them? I thought
    it was unusual that the majority of listings have the minimum stay
    at a month, but I guess in LA a lot of people either vacation or
    work there for short periods of time, so they are able to rent out
    their houses for longer periods, like a month, for other people
    looking for extended vacations or work.

Perform an analysis of the variation in the “number\_of\_reviews”
column. Make sure to explore different “binwidth” values in your
analysis.

``` r
ggplot(listings) +
  geom_histogram(aes(x = number_of_reviews), binwidth = 1)
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = number_of_reviews), binwidth = 10)
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-2.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = number_of_reviews), binwidth = 50)
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-3.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = number_of_reviews), binwidth = 1) +
  coord_cartesian(xlim = c(0,50))
```

![](Exploring_files/figure-gfm/unnamed-chunk-8-4.png)<!-- -->

  - Which values are the most common? Why?

> The most common values occur between -.5 and .5. Looking at the data,
> most of the listings do not have any reviews. This is most likely
> because people do not want to take the time to review the place they
> stayed in. As long as their stay was not exceptional or horrible, most
> people don’t particularly care.

  - Which values are rare? Why? Does that match your expectations?

> As the number of reviews increases, the count decreases. This matches
> my expectations because obviously since many listings don’t have any
> reviews, the amount of people leaving reviews on listings is not very
> high.

  - Can you see any unusual patterns? What might explain them?

> No unusual patterns. There are small spikes in places like 26 reviews
> and 32 reviews, but these are random and do not form a pattern.

Perform an analysis of the variation in the “availability\_365” column.
Make sure to explore different “binwidth” values in your analysis.

``` r
ggplot(listings) +
  geom_histogram(aes(x = availability_365), binwidth = 1)
```

![](Exploring_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = availability_365), binwidth = 10)
```

![](Exploring_files/figure-gfm/unnamed-chunk-9-2.png)<!-- -->

``` r
ggplot(listings) +
  geom_histogram(aes(x = availability_365), binwidth = 20)
```

![](Exploring_files/figure-gfm/unnamed-chunk-9-3.png)<!-- -->

  - Which values are the most common? Why?

> The most common value is 0, but there are increases at around 90, 175,
> and 365. These trends are most likely seasonal, as people will
> generally fit into one of a few categories: live in LA but are renting
> out house once, live in LA 2/3 of the year but have a vacation home
> for the winter/summer, live elsewhere and have a vacation house in LA
> that they can rent 2/3 of the year, or own properties specifically for
> Airbnb that are available year round.

  - Which values are rare? Why? Does that match your expectations?

> Values in between these seasonal spikes are pretty rare, because most
> people fit into those categories.

  - Can you see any unusual patterns? What might explain them?

> No unusual patterns, just the one mentioned before. It is weird,
> however, that there are values of 0, because if it is never available
> then it should not be listed on Airbnb

### Part II

What is the most common name (of a person) in the city you selected

``` r
count(listings, host_name) %>%
  arrange(desc(n))
```

    ## # A tibble: 7,097 x 2
    ##    host_name      n
    ##    <chr>      <int>
    ##  1 PCHSoCal     308
    ##  2 David        287
    ##  3 Alex         244
    ##  4 Michael      228
    ##  5 Blueground   206
    ##  6 James        166
    ##  7 John         159
    ##  8 Mark         154
    ##  9 Sarah        152
    ## 10 Nicole       147
    ## # … with 7,087 more rows

Do the number of reviews affect the price of the Airbnb? How? Why do you
think this happens?

``` r
listings2 <- filter(listings, price <= 1000)
ggplot(listings2, aes(x = number_of_reviews, y = price)) +
  geom_point() +
  geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'gam' and formula 'y ~ s(x, bs = "cs")'

![](Exploring_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

> As indicated by the trend line, there does not appear to be a linear
> correlation between number of reviews and price in LA. While the most
> expensive listings tend to have very few reviews, this is most likely
> due to limited traffic and a smaller number of people renting these
> listings.

What type of room tends to have the highest Airbnb price?

``` r
ggplot(listings2, aes(x = room_type, y = price)) +
  geom_boxplot()
```

![](Exploring_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

> The room type with the highest median price is entire homes/apts,
> which makes sense, as you can charge more for a full home as opposed
> to a hotel room or just a room in someone’s house.

What neighborhoods tend to have the highest Airbnb price?

``` r
ggplot(listings2) +
  geom_boxplot(aes(x = reorder(neighbourhood, price, FUN = median), y = price)) +
  coord_flip()
```

![](Exploring_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

``` r
by_neighborhood <- group_by(listings, neighbourhood) %>%
  summarize(avg_price = mean(price)) %>%
  arrange(desc(avg_price))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

``` r
by_neighborhood
```

    ## # A tibble: 263 x 2
    ##    neighbourhood                         avg_price
    ##    <chr>                                     <dbl>
    ##  1 Rolling Hills                             2668.
    ##  2 Bel-Air                                   2609.
    ##  3 Malibu                                    1639.
    ##  4 Beverly Crest                             1249.
    ##  5 Hollywood Hills West                       901.
    ##  6 Beverly Hills                              846.
    ##  7 Westlake Village                           740.
    ##  8 Unincorporated Santa Monica Mountains      706.
    ##  9 Florence-Firestone                         639.
    ## 10 Avalon                                     504.
    ## # … with 253 more rows

> The most famous neighborhoods in LA have the highest average price,
> like Bel-Air, Malibu, and the Hollywood Hills. While there are fewer
> listings in these areas, their reputation allows owners to charge
> higher for Airbnbs.

Suppose you could purchase a property in the city you selected, and that
you could rent it to others as an Airbnb. In what neighborhood would you
want to purchase your property? Why?

``` r
group_by(listings, neighbourhood) %>%
  count(neighbourhood) %>%
  arrange(desc(n))
```

    ## # A tibble: 263 x 2
    ## # Groups:   neighbourhood [263]
    ##    neighbourhood       n
    ##    <chr>           <int>
    ##  1 Long Beach       1584
    ##  2 Venice           1571
    ##  3 Hollywood        1525
    ##  4 Santa Monica     1139
    ##  5 Downtown         1110
    ##  6 Hollywood Hills   721
    ##  7 West Hollywood    618
    ##  8 Glendale          560
    ##  9 Rowland Heights   521
    ## 10 Beverly Hills     511
    ## # … with 253 more rows

> I would purchase my property in Bel-Air because it has the second
> highest average price, but since it is a notoriously nice
> neighborhood, I could upcharge renters. Bel-Air also has the lowest
> amount of listings out of neighborhoods in the top 10 in average
> price. This means there there is less competition, and I would be one
> of the only options in the area, so again I could upcharge

### Part III

Visit a real estate website and find a property that is for sale in the
neighborhood you selected. Take note of the price and address of the
property.

2564 Basil Ln, Los Angeles, CA, 90077. The House is $1,449,000.

Use your dataset to find what the average Airbnb price/night is in the
neighborhood you selected.

``` r
by_neighborhood
```

    ## # A tibble: 263 x 2
    ##    neighbourhood                         avg_price
    ##    <chr>                                     <dbl>
    ##  1 Rolling Hills                             2668.
    ##  2 Bel-Air                                   2609.
    ##  3 Malibu                                    1639.
    ##  4 Beverly Crest                             1249.
    ##  5 Hollywood Hills West                       901.
    ##  6 Beverly Hills                              846.
    ##  7 Westlake Village                           740.
    ##  8 Unincorporated Santa Monica Mountains      706.
    ##  9 Florence-Firestone                         639.
    ## 10 Avalon                                     504.
    ## # … with 253 more rows

> The average Airbnb price per night is $2609.46 in Bel-Air

Use your dataset to find what the average number of available nights per
year is for an Airbnb in the neighborhood you selected.

``` r
group_by(listings, neighbourhood) %>%
  summarize(avg_available = mean(availability_365)) %>%
  arrange(desc(avg_available))
```

    ## `summarise()` ungrouping output (override with `.groups` argument)

    ## # A tibble: 263 x 2
    ##    neighbourhood             avg_available
    ##    <chr>                             <dbl>
    ##  1 East Compton                       361 
    ##  2 Whittier Narrows                   346 
    ##  3 Griffith Park                      342.
    ##  4 Watts                              329.
    ##  5 Green Meadows                      322 
    ##  6 Northeast Antelope Valley          318.
    ##  7 San Fernando                       310 
    ##  8 Desert View Highlands              306.
    ##  9 Avalon                             298.
    ## 10 Sepulveda Basin                    297 
    ## # … with 253 more rows

> The average Airbnb availability in Bel-Air is 236.5 nights per year.

Suppose you bought the property above. If you were to rent it as an
Airbnb at the average neighborhood price, for the average number of
days, how long will it take you to break even.

``` r
1449000 / 2609.46
```

    ## [1] 555.2873

``` r
555.2873/236.5
```

    ## [1] 2.347938

> It would take 555.29 days of renting to break even, and with an
> average availability of 236.5 nights, I would break even in about 2.35
> years.

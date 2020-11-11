Data Visualization
================
Matt Fleming
8/21/20

# Data Visualization

### 3.1 Introduction

``` r
# we must load the tidyverse library every session
library(tidyverse)
```

    ## ── Attaching packages ───────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ──────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

### 3.2 First Steps

QUESTION: Do cars with big engines use more gas than cars with small
engines?

##### 3.2.1 The mpg data frame

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

##### 3.2.2 Creating a ggplot

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

This plot defends the hypothesis that cars with larger engines will
generally have worse fuel efficiency.

##### 3.2.4 Exercises

> 1.  Run ggplot(data = mpg). What do you see?

There is a blank graph since we have not mapped any data points.

``` r
ggplot(data = mpg)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

> 2.  How many rows are in mpg? How many columns?

234 and 11

``` r
mpg
```

    ## # A tibble: 234 x 11
    ##    manufacturer model    displ  year   cyl trans   drv     cty   hwy fl    class
    ##    <chr>        <chr>    <dbl> <int> <int> <chr>   <chr> <int> <int> <chr> <chr>
    ##  1 audi         a4         1.8  1999     4 auto(l… f        18    29 p     comp…
    ##  2 audi         a4         1.8  1999     4 manual… f        21    29 p     comp…
    ##  3 audi         a4         2    2008     4 manual… f        20    31 p     comp…
    ##  4 audi         a4         2    2008     4 auto(a… f        21    30 p     comp…
    ##  5 audi         a4         2.8  1999     6 auto(l… f        16    26 p     comp…
    ##  6 audi         a4         2.8  1999     6 manual… f        18    26 p     comp…
    ##  7 audi         a4         3.1  2008     6 auto(a… f        18    27 p     comp…
    ##  8 audi         a4 quat…   1.8  1999     4 manual… 4        18    26 p     comp…
    ##  9 audi         a4 quat…   1.8  1999     4 auto(l… 4        16    25 p     comp…
    ## 10 audi         a4 quat…   2    2008     4 manual… 4        20    28 p     comp…
    ## # … with 224 more rows

> 3.  What does the drv variable describe? Read the help for ?mpg to
>     find out.

Type of drive train i.e. front wheel drive, four wheel drive, rear wheel
drive

``` r
?mpg
```

> 4.  Make a scatterplot of hwy vs cyl.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = hwy, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

> 5.  What happens if you make a scatterplot of class vs drv? Why is the
>     plot not useful?

It does not show a correlation but instead a random series of points.
Since both variables are categorical there is no way to show how often
each type of car occurs.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = class, y = drv))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

### 3.3 Aesthetic mappings

You can convey information about your data by mapping the aesthetics in
your plot to the variables in your dataset. For example, you can map the
colors of your points to the class variable to reveal the class of each
car.

To map an aesthetic to a variable, associate the name of the aesthetic
to the name of the variable inside aes(). ggplot2 will automatically
assign a unique level of the aesthetic (here a unique color) to each
unique value of the variable, a process known as scaling. ggplot2 will
also add a legend that explains which levels correspond to which values.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

This plot maps class to the size aesthetic, which is not reccommended
and prompts a warning to appear.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = class))
```

    ## Warning: Using size for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

This plot maps the alpha aesthetic, which changes transparency in the
mapped points.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, alpha = class))
```

    ## Warning: Using alpha for a discrete variable is not advised.

![](Data-Visualization_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

This plot shows us why the shape aesthetic is flawed, as only six shapes
can be used at once and we lose all of the suv class points.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, shape = class))
```

    ## Warning: The shape palette can deal with a maximum of 6 discrete values because
    ## more than 6 becomes difficult to discriminate; you have 7. Consider
    ## specifying shapes manually if you must have them.

    ## Warning: Removed 62 rows containing missing values (geom_point).

![](Data-Visualization_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

Using quotations allows us to manually control the aesthetic and select
one aesthetic for all points.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

##### 3.3.1 Exercises

> 1.  What’s gone wrong with this code? Why are the points not blue?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Since blue is included in the aesthetic, it maps blue as a relation
between a variable and a value.

> 2.  Which variables in mpg are categorical? Which variables are
>     continuous? (Hint: type ?mpg to read the documentation for the
>     dataset). How can you see this information when you run mpg?

manufacturer, model, year, cyl, trans, drv, fl, class are categorical,
the rest are continuous

``` r
?mpg
```

> 3.  Map a continuous variable to color, size, and shape. How do these
>     aesthetics behave differently for categorical vs. continuous
>     variables?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, size = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = cty))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
# This chuck is supposed to have shape = cty showing us why continuous variables cannot be mapped to shape but that won't knit so I removed it.
```

> 4.  What happens if you map the same variable to multiple aesthetics?

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = cyl, size = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

> 5.  What does the stroke aesthetic do? What shapes does it work with?
>     (Hint: use ?geom\_point)

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, stroke = year))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

> 6.  What happens if you map an aesthetic to something other than a
>     variable name, like aes(colour = displ \< 5)? Note, you’ll also
>     need to specify x and y.

The aesthetic is mapped as an equation, and points that are true satisfy
the equation.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = displ < 5))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

### 3.5 Facets

Adding facets splits the plot into subsets that display one group of
data from the whole set. Faceted variable must be discrete.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

Facet grid is used to create more subsets of data divided by two
variables.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

. can be used in place of a variable in facet grid.

##### 3.5.1 Exercises

> 1.  What happens if you facet on a continuous variable?

The continuous variable is divided by each value that is represented by
the data.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ cty)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

> 2.  What do the empty cells in plot with facet\_grid(drv \~ cyl) mean?
>     How do they relate to this plot?

The empty cells represent an absence of data, for example, there are no
cars with rear wheel drive and 4 cylinder engines in the data. The empty
cells are similar to this graph that lacks data points on 4 cylinder
rear wheel drive cars.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = drv, y = cyl))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

> 3.  What plots does the following code make? What does . do?

. takes the place of the variable you replace it with, removing a
division of the facet grid. Basically a facet wrap but easier to control
x and y.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(drv ~ .)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_grid(. ~ cyl)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

> 4.  Take the first faceted plot in this section:

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + facet_wrap(~ class, nrow = 2)
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

What are the advantages to using faceting instead of the colour
aesthetic? What are the disadvantages? How might the balance change if
you had a larger dataset? While the color aesthetic allows user to
visualize a third variable in the overall data set, faceting allows user
to use the third variable to split the data up and look at independent
graphs based on the third variable. In a larger data set,

Faceting makes the data easier to visualize when divided by more
variables. While the color aesthetic allows user to visualize different
categories in the same plot, faceting divides the plots and allows user
to compare the trends of similar variables in separate categories.
Faceting should generally be more useful in larger datasets since
individual points are harder to visualize if they are overlapping or
similar. The main disadvantage of faceting is in the case of smaller
datasets where the data is divided and it is more difficult to visualize
trends.

> 5.  Read ?facet\_wrap. What does nrow do? What does ncol do? What
>     other options control the layout of the individual panels? Why
>     doesn’t facet\_grid() have nrow and ncol arguments?

In the facet wrap nrow and ncol lets you pick how many rows and columns
the data will be divided into. Facet grid does not have this option
since the data is automatically divided based on the amount of
variables.

``` r
?facet_wrap
```

> 6.  When using facet\_grid() you should usually put the variable with
>     more unique levels in the columns. Why?

It is easier to visualize the data when it is neat and wider across as
opposed to a straight up and down grid that you have to scroll to see.

### 3.6 Geometric Objects

Changing the geom changes the object used to map the plot. For example,
geom\_bar maps bar charts.

This geom\_smooth maps a line.

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

Different aesthetics work for different geoms. For example, changing
shape aesthetic works for a scatterplot because you can change the shape
of each point, but the line doesn’t show points so the shape aesthetic
won’t work for geom\_smooth. However, changing the line type provides a
similar function for smooth. This ggplot divides the lines by drive
train.

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, linetype = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, group = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->

This plot has both smooth and point geoms, so it maps the line and the
scatterplot, allowing user to compare the raw data with a line of best
fit.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy)) + geom_smooth(mapping = aes(x = displ, y =hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-34-1.png)<!-- -->

This ggplot serves the same purpose as the last, but additionally
separates the data by color.

``` r
ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy, color = drv)) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-35-1.png)<!-- -->

Another way to write this code and apply certain mappings to all geoms
is to write the mapping in the ggplot.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->

This ggplot has universally applied mappings in addition to mappings
that only apply to the geom point. With this code, you can apply
mappings to the layers you want while avoiding repetition.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_smooth() + geom_point(mapping = aes(color = class))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-37-1.png)<!-- -->

## Exercises 1-5

> 1.  What geom would you use to draw a line chart? A boxplot? A
>     histogram? An area chart?

geom\_line, geom\_boxplot, geom\_histogram, geom\_area

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_area()
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-38-1.png)<!-- -->

> 2.  Run this code in your head and predict what the output will look
>     like. Then, run the code in R and check your predictions.

scatterplot and smooth line, the se = false removes standard error so
there is no shaded area showing error.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + geom_point() + geom_smooth(se = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-39-1.png)<!-- -->

> 3.  What does show.legend = FALSE do? What happens if you remove it?
>     Why do you think I used it earlier in the chapter?

This removes the legend or key.

``` r
ggplot(data = mpg) + geom_smooth(mapping = aes(x = displ, y = hwy, color = drv), show.legend = FALSE)
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-40-1.png)<!-- -->

> 4.  What does the se argument to geom\_smooth() do?

It displays the standard margin of error.

> 5.  Will these two graphs look different? Why/why not?

They will look the same because they both have the same mappings, but
the first universally applies the mappings while the second individually
applies them.

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point() + geom_smooth()
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-41-1.png)<!-- -->

``` r
ggplot() + geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](Data-Visualization_files/figure-gfm/unnamed-chunk-42-1.png)<!-- -->

### 3.7 Statistical Transformations

``` r
?diamonds
```

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-44-1.png)<!-- -->

### 3.8 Position Adjustments

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = cut))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-45-1.png)<!-- -->

``` r
ggplot(data = diamonds) + geom_bar(mapping = aes(x = cut, fill = clarity))
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(alpha = 0.2, position = "identity")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, color = clarity)) + geom_bar(fill = NA, position = "identity")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "fill")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

``` r
ggplot(data = diamonds, mapping = aes(x = cut, fill = clarity)) + geom_bar(position = "dodge")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point()
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + geom_point(position = "jitter")
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

##### 3.8.1 Exercises

> 1.  What is the problem with this plot? How could you improve it?

``` r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + geom_point()
```

![](Data-Visualization_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

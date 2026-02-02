Lab 02 - Plastic waste
================
Tsion
01/31/2026

## Load packages and data

``` r
library(tidyverse) 
```

``` r
plastic_waste <- read.csv("data/plastic-waste.csv")
```

Data Visualization: (Before starting exercise: For my own practice and
to look back on later)

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](lab-02_files/figure-gfm/histogram%20of%20distribution%20of%20plastic%20waste%20per%20capita-1.png)<!-- -->

``` r
plastic_waste %>%
  filter(plastic_waste_per_cap > 3.5)
```

    ##   code              entity     continent year gdp_per_cap plastic_waste_per_cap
    ## 1  TTO Trinidad and Tobago North America 2010    31260.91                   3.6
    ##   mismanaged_plastic_waste_per_cap mismanaged_plastic_waste coastal_pop
    ## 1                             0.19                    94066     1358433
    ##   total_pop
    ## 1   1341465

## Exercises

### Exercise 1

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2) + 
  facet_wrap(~continent)
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- -->


    ### Exercise 2


    ``` r
    ggplot(
      data = plastic_waste,
      mapping = aes(
        x = plastic_waste_per_cap,
        color = continent,
        fill = continent
      )
    ) +
      geom_density(alpha = 0.3)

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density,%20better%20alpha-1.png)<!-- -->

2.2. The reason why we defined ‘color’ and ‘fill’ under mapping
aesthetics of the plot is becuase these are characteristics that are
based on (vary by) the vaues in the data (for example here different
color and fill for each continent). On the other hand, for the alpa,
this is a characteristics that is not based on the values of the data
for our current purpose (we are changing the transparency level of the
fill color to help with the overlapping colors of the continents making
it hard to effectively visualize the data).

### Exercise 3

Remove this text, and add your answer for Exercise 3 here.

``` r
# insert code here
```

### Exercise 4

Remove this text, and add your answer for Exercise 4 here.

``` r
# insert code here
```

``` r
# insert code here
```

``` r
# insert code here
```

``` r
# insert code here
```

### Exercise 5

Remove this text, and add your answer for Exercise 5 here.

``` r
# insert code here
```

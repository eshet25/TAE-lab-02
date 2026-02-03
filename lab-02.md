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

It was actually quite a surpirse for me to see Trinidad and Tobago as
the outlier here, especially comparing it to larger and more industrial
countries like China, and India. I looked it up to and found this Forbes
article published in 2019:
<https://www.forbes.com/sites/daphneewingchow/2019/09/20/caribbean-islands-are-the-biggest-plastic-polluters-per-capita-in-the-world/>.

It mentioned that majority of the Carribean countries are ranked amongst
the countries with highest plastic pollution (10 Carribean countries
ranked out of the top 30 global polluters per capita), with Trinidad and
Tobago being the first one. The main issue lies in inadequate waste
management since the small populations Trinidad and Tobago combined with
the high consumption increases their rates much higher. They produce
much more plastic waste per person than any other country (0.19 kg per
person per day. Most of their plastic waste is being disposed inproperly
to the ocean, which results in “more marine plastic originating in
Trinidad & Tobago (per capita) than 98% of the countries in the world.”
So, unfortunately I’d say, the data we see here is certainly showing
real phenomenon rather than an error.

``` r
ggplot(data = plastic_waste, aes(x = plastic_waste_per_cap)) +
  geom_histogram(binwidth = 0.2) + 
  facet_wrap(~continent) + 
  labs( 
    title = "Distribution of plastic waste per capita",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Countries (count)"
    )
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_bin()`).

![](lab-02_files/figure-gfm/plastic-waste-continent-1.png)<!-- -->

It looks like the plastic waste per capita levels are mostly on the
lower levels for most of the countries. Africa seems to have the lowest
plastic waste skewed to the right. Oceania and South America also show
generally low-to-moderate levels of plastic waste per capita, but their
histograms are less dense, probably because they have less countries.
Asia, and Europe also show lower-to-moderate levels. North American
countries are also generally low-to-moderate with the Trinidad and
Tobago as the higher outlier.

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
  geom_density(alpha = 0.3) + 
  labs (
  title = "Distribution of plastic waste per capita",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Countries (density)")
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_density()`).

![](lab-02_files/figure-gfm/plastic-waste-density,%20better%20alpha-1.png)<!-- -->

2.2. The reason why we defined ‘color’ and ‘fill’ under mapping
aesthetics of the plot is because these are characteristics that are
based on (vary by) the values in the data (for example here, different
color and fill show each continent). On the other hand, for the alpha,
this is a characteristics that is not based on the values of the data
for our current purpose (we are changing the transparency level of the
fill color to help with the overlapping colors of the continents making
it hard to effectively visualize the data). So, we define it here a a
characteristic of the plotting geom (setting).

### For my own practice (to refer back later)

``` r
ggplot(
  data = plastic_waste,
  mapping = aes(
    x = continent,
    y = plastic_waste_per_cap
  )
) +
  geom_boxplot() +
  labs (
  title = "Boxplot distribution of plastic waste per capita",
    subtitle = "by continent",
    x = "Continents",
    y = "Plastic waste per capita (kg/day)")
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](lab-02_files/figure-gfm/plastic-waste-box%20plots-1.png)<!-- -->

\*Note: To zoom in to the box plots and not have it compressed by the
outlier, you can add:

``` r
ggplot(
  data = plastic_waste,
  mapping = aes(
    x = continent,
    y = plastic_waste_per_cap
  )
) +
   geom_boxplot(width = 0.7) +
  coord_cartesian(ylim = c(0, 0.6)) +
  labs (
  title = "Boxplot distribution of plastic waste per capita",
    subtitle = "by continent",
    x = "Continents",
    y = "Plastic waste per capita (kg/day)")
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_boxplot()`).

![](lab-02_files/figure-gfm/plastic-waste-zoom%20in-box%20plots-1.png)<!-- -->

### Exercise 3

``` r
ggplot(
  data = plastic_waste,
  mapping = aes(
    x = continent,
    y = plastic_waste_per_cap
  )
) +
  geom_violin() +
  labs (
  title = "Violin distribution of plastic waste per capita",
    subtitle = "by continent",
    x = "Continents",
    y = "Plastic waste per capita (kg/day)")
```

    ## Warning: Removed 51 rows containing non-finite outside the scale range
    ## (`stat_ydensity()`).

![](lab-02_files/figure-gfm/plastic-waste-violin-1.png)<!-- -->

3.1. The violin distributions give us more information about the shape
of the distriution, compared to box plots. Violin plots are a
combination of a box plot and density plot. For example, if we look at
the plot for Africa, we can see that it is wider at the bottom (a
triangle shape), which shows us that most countires in Africa are in the
low range for plastic waste per cap.

On the other hand, violin plots aren’t as effective as box plots when it
comes to identifying outliers, and also if we want to present a more
simplified way to visualize/interpret data. So, it depends on our goal
which one we would like to use, as they both have their own advantages.

### Exercise 4

### 4.1

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = mismanaged_plastic_waste_per_cap
)
) + 
geom_point() +
labs (
  title = "Scatterplot: Plastic Waste vs Mismanaged plastic waste per capita",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Mismanaged plastic waste per capita (kg/day)")
```

    ## Warning: Removed 51 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-1.png)<!-- -->

Most countries seem to be piled up near the lower values of plastic
waste per capita. It appears like there is some upward trend going on in
the lower values, but we can’t know much at this point since there is no
distinction between the continents. As we saw from previous
visualizations, we can also see clearly there is one clear outlier that
is further out more than 3kg/day.

### 4.2

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = mismanaged_plastic_waste_per_cap,
color = continent
)
) + 
geom_point()  +
labs (
  title = "Scatterplot: Plastic Waste vs Mismanaged plastic waste per capita",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Mismanaged plastic waste per capita (kg/day)")
```

    ## Warning: Removed 51 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-mismanaged-continent-1.png)<!-- -->

I don’t think there is a very obvious distinction between the continents
since they are very clustered together. But it also looks like most
continents follow somewhat upward of a pattern.As the plastic waste per
capita increases, there mostly seems to be an increase with the
mismanaged plastic waste per capita for the continents (the least
obvious in this trend seems to be South America). The extreme outlier we
idenitifed belongs to North America.

### 4.3

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = total_pop,
color = continent
)
) + 
geom_point()  +
labs (
  title = "Scatterplot: Plastic Waste per capita vs Total Population",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Total Population")
```

    ## Warning: Removed 61 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-population-total-1.png)<!-- -->

There doesn’t seem to be a clear/strong linear relationship, it’s not
very clear since they are clustered very much. We can try to do facet to
see better

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = total_pop,
color = continent
)
) + 
geom_point(size = 1)  +
facet_wrap(~ continent) +
labs (
  title = "Scatterplot: Plastic Waste per capita vs Total Population",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Total Population")
```

    ## Warning: Removed 61 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-population-total%20facet-1.png)<!-- -->

I still can’t confidently say I can see a very clear linear
relationship. In Asia, we can see a couple of countries that are in the
higher population range (\>1,000,000,000), but are still showing low
plastic waste per capita. Most countries in each continent are clustered
at the lower values of plastic waste per capita, and generally in the
population range of \< 500,000,000. In North America, it looks like most
of the countries are concentrated in the very low total population range
(0e+00).

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = coastal_pop,
color = continent
)
) + 
geom_point() +
labs (
  title = "Scatterplot: Plastic Waste per capita vs Coastal Population",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Coastal Population")
```

    ## Warning: Removed 51 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-population-coastal-1.png)<!-- -->

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = plastic_waste_per_cap,
y = coastal_pop,
color = continent
)
) + 
geom_point() +
facet_wrap(~ continent) +
labs (
  title = "Scatterplot: Plastic Waste per capita vs Coastal Population",
    subtitle = "by continent",
    x = "Plastic waste per capita (kg/day)",
    y = "Coastal Population")
```

    ## Warning: Removed 51 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/plastic-waste-population-coastal%20facet-1.png)<!-- -->

Here as well, I am not sure if I see a clear/strong linear assosciation.
Most of the countries are clustered around the lower pastic per waste
capita values, and with generally low coastal population. But in Asia,
we see a number of countries that have high coastal population but are
still in the lower range for plastic waste per capita.

### Exercise 5

\*Note: group =1, makes one smooth line for all continents (instead of
separate lines)

\*se = TRUE, shows the confidence interval around the smooth line

``` r
ggplot (
data = plastic_waste,
mapping = aes(
x = coastal_pop/ total_pop,
y = plastic_waste_per_cap,
color = continent
)
) + 
geom_point () +
geom_smooth(
aes (group = 1),
color = "black",
se = TRUE
) +
scale_color_viridis_d() +
coord_cartesian(ylim = c(0,0.7)) +
labs (
  title = "Plastic Waste vs coastal population proportion",
    subtitle = "by continent",
    x = "Coastal population proportion (Coastal/ total population",
    y = "Plastic waste per capita (kg/day)",
    color = "Continents") +
    theme_minimal()
```

    ## `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

    ## Warning: Removed 61 rows containing non-finite outside the scale range
    ## (`stat_smooth()`).

    ## Warning: Removed 61 rows containing missing values or values outside the scale range
    ## (`geom_point()`).

![](lab-02_files/figure-gfm/recreate-viz-1.png)<!-- -->

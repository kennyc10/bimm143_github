# Class 05 BIMM 143


- [background](#background)
- [Using different Geoms](#using-different-geoms)

# background

there are many graphic systems avaialble in R . these functions include
” base R” and tons of add on ackages like “ggplot2”

Lets Compare “base” and ggplot2: briefly: we can use some example data
that is built in with R called Cars

``` r
head(cars)
```

      speed dist
    1     4    2
    2     4   10
    3     7    4
    4     7   22
    5     8   16
    6     9   10

In base r I can just call ‘plot()’

``` r
plot(cars)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-2-1.png)

now we can do this with ggplot2

First we need to install the package . we do this by
’install.packages(“ggplot2”)i only need to do this once and then it
stays on my computer

> Key Point: I only install packages in the R consle and not the rs
> script or quarto doc.

before i use any add on package i must load it with a call to library()

library(ggplot2) ggplot(cars)

``` r
library(ggplot2) 
ggplot(cars)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-3-1.png)

How can we do this with **ggplot** \# First we need to install package.
we do this ’install.packages(“ggplot2”). i only meed to do this once and
then it will be available on my computer from then on \# key point : i
only install packages in the R console not withing quarto docs or R
scripts

Before I can use any add on package I must upload it with a call on
’library()

every ggplot has at least 3 things: - the **data** ( in our case
‘cars’) - the **aes**thetics (how the data amp to the plot) - How
**geom**s that determined how the plot is drawn (line, points columns,
etc.)

``` r
ggplot(cars) + 
aes(x=speed, y=dist) + 
geom_point() + 
geom_smooth(se=FALSE)
```

    `geom_smooth()` using method = 'loess' and formula = 'y ~ x'

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-4-1.png)

for “simple” plots ggplots is much more verbose than base R but the
defaults are nicer and for comlpicated plots it becomes mcuh more
efficent and structural

add a line to show relationship of speed to stopping distance (i.e. add
another “layer”)

> Q. add a title and subtile to the plot

using different aes and geoms I can add always save my ggplot

> Q. add a title and subtile to the plot

``` r
p <- ggplot(cars, aes(x = speed, y = dist)) +
  geom_point()
p + 
labs(title= "my first ggplot",
subtitle = "stopping distance of old cars", 
caption= "BIMM 143", 
x= "speed(MPG)", 
y= "stopping Distance (ft)") + 
theme_bw()
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-5-1.png)

``` r
url <- "https://bioboot.github.io/bimm143_S20/class-material/up_down_expression.txt" 
genes <- read.delim(url) 
head(genes)
```

            Gene Condition1 Condition2      State
    1      A4GNT -3.6808610 -3.4401355 unchanging
    2       AAAS  4.5479580  4.3864126 unchanging
    3      AASDH  3.7190695  3.4787276 unchanging
    4       AATF  5.0784720  5.0151916 unchanging
    5       AATK  0.4711421  0.5598642 unchanging
    6 AB015752.4 -3.6808610 -3.5921390 unchanging

# Using different Geoms

\#let’s Plot some aspects of the in-built “mtcars”

``` r
head(mtcars)
```

                       mpg cyl disp  hp drat    wt  qsec vs am gear carb
    Mazda RX4         21.0   6  160 110 3.90 2.620 16.46  0  1    4    4
    Mazda RX4 Wag     21.0   6  160 110 3.90 2.875 17.02  0  1    4    4
    Datsun 710        22.8   4  108  93 3.85 2.320 18.61  1  1    4    1
    Hornet 4 Drive    21.4   6  258 110 3.08 3.215 19.44  1  0    3    1
    Hornet Sportabout 18.7   8  360 175 3.15 3.440 17.02  0  0    3    2
    Valiant           18.1   6  225 105 2.76 3.460 20.22  1  0    3    1

> Q. scatters plot of ‘mpg’ vs ‘disp’

> Q. boxplot of ‘gear’ vs ‘disp’

> Q. barplot of ‘carb’

> Q. Smoothh of ‘Disp’ vs ‘qsec’

``` r
ggplot 
```

    function (data = NULL, mapping = aes(), ..., environment = parent.frame()) 
    {
        UseMethod("ggplot")
    }
    <bytecode: 0x1239567e0>
    <environment: namespace:ggplot2>

``` r
url <- "https://bioboot.github.io/bimm143_S20/class-material/up_down_expression.txt" 
genes <- read.delim(url) 
head(genes)
```

            Gene Condition1 Condition2      State
    1      A4GNT -3.6808610 -3.4401355 unchanging
    2       AAAS  4.5479580  4.3864126 unchanging
    3      AASDH  3.7190695  3.4787276 unchanging
    4       AATF  5.0784720  5.0151916 unchanging
    5       AATK  0.4711421  0.5598642 unchanging
    6 AB015752.4 -3.6808610 -3.5921390 unchanging

``` r
table(genes$States)
```

    < table of extent 0 >

``` r
ggplot(genes) + 
aes(x=Condition1, y=Condition2, col=State) + 
scale_color_manual(values=c( "blue", "yellow", "red")) + 
geom_point()
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-10-1.png)

``` r
# File location online
url <- "https://raw.githubusercontent.com/jennybc/gapminder/master/inst/extdata/gapminder.tsv"

gapminder <- read.delim(url)
```

``` r
# install.packages("dplyr")  ## un-comment to install if needed
library(dplyr)
```


    Attaching package: 'dplyr'

    The following objects are masked from 'package:stats':

        filter, lag

    The following objects are masked from 'package:base':

        intersect, setdiff, setequal, union

``` r
gapminder_2007 <- gapminder %>% filter(year==2007)
```

``` r
ggplot(gapminder_2007) +
  aes(x=gdpPercap, y=lifeExp) +
  geom_point()
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-14-1.png)

``` r
ggplot(gapminder_2007) +
  aes(x=gdpPercap, y=lifeExp) +
  geom_point(alpha=0.5)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-15-1.png)

``` r
ggplot(gapminder_2007) +
  aes(x=gdpPercap, y=lifeExp, color=continent, size=pop) +
  geom_point(alpha=0.5)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-16-1.png)

``` r
ggplot(gapminder_2007) + 
  aes(x = gdpPercap, y = lifeExp, color = pop) +
  geom_point(alpha=0.8)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-17-1.png)

``` r
ggplot(gapminder_2007) + 
  aes(x = gdpPercap, y = lifeExp, size = pop) +
  geom_point(alpha=0.5)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-18-1.png)

``` r
ggplot(gapminder_2007) + 
  geom_point(aes(x = gdpPercap, y = lifeExp,
                 size = pop), alpha=0.5) + 
  scale_size_area(max_size = 10)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-19-1.png)

``` r
gapminder_1957 <- gapminder %>% filter(year==1957)

ggplot(gapminder_1957) + 
  aes(x = gdpPercap, y = lifeExp, color=continent,
                 size = pop) +
  geom_point(alpha=0.7) + 
  scale_size_area(max_size = 10) 
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-20-1.png)

``` r
gapminder_1957 <- gapminder %>% filter(year==1957 | year==2007)

ggplot(gapminder_1957) + 
  geom_point(aes(x = gdpPercap, y = lifeExp, color=continent,
                 size = pop), alpha=0.7) + 
  scale_size_area(max_size = 10) +
  facet_wrap(~year)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-21-1.png)

``` r
library(gapminder)
```


    Attaching package: 'gapminder'

    The following object is masked _by_ '.GlobalEnv':

        gapminder

``` r
library(gganimate)

# Setup nice regular ggplot of the gapminder data
ggplot(gapminder, aes(gdpPercap, lifeExp, size = pop, colour = country)) +
  geom_point(alpha = 0.7, show.legend = FALSE) +
  scale_colour_manual(values = country_colors) +
  scale_size(range = c(2, 12)) +
  scale_x_log10() +
  facet_wrap(~continent) +
  labs(title = 'Year: {frame_time}', x = 'GDP per capita', y = 'life expectancy') +
  transition_time(year) +
  shadow_wake(wake_length = 0.1, alpha = FALSE)
```

![](BIMM-class-05_files/figure-commonmark/unnamed-chunk-22-1.gif)

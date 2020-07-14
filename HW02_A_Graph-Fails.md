What went wrong?
================
Robert Gruener

``` r
knitr::opts_chunk$set(echo = TRUE, error = TRUE)
```

## HW02 Part A

In this document, I will add some examples of some coding mistakes, it
is up to you to figure out why the graphs are messing up.

### First load packages

It is always best to load the packages you need at the top of a script.
It’s another common coding formatting standard (like using the
assignment operator instead of the equals sign). In this case, it helps
people realize what they need to install for the script and gives an
idea of what functions will be called.

It is also best coding practice to only call the packages you use, so if
you use a package but end up tossing the code you use for it, then make
sure to remove loading it in the first place. For example, I could use
`library("tidyverse")` but since this script will only be using ggplot2,
I only load ggplot2.

``` r
library("ggplot2")
library("magrittr") #so I can do some piping
```

### Graph Fail 1

What error is being thrown? How do you correct it? (hint, the error
message tells you)

> used `%>%` when should have used `+`

> also, used incorrect vairable name `city` instead of `cty`

``` r
data(mpg) #this is a dataset from the ggplot2 package

mpg %>% 
  ggplot(mapping = aes(x = cty, y = hwy, color = "blue")) + 
  geom_point()
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

### Graph Fail 2

Why aren’t the points blue? It is making me blue that the points in the
graph aren’t blue :\`(

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Graph Fail 3

Two mistakes in this graph. First, I wanted to make the the points
slightly bolder, but changing the alpha to 2 does nothing. What does
alpha do and what does setting it to 2 do? What could be done instead if
I want the points slightly bigger?

> alpha is the opacity value, with 0 being totally transparent and 1
> being opaque.

Second, I wanted to move the legend on top of the graph since there
aren’t any points there, putting it at approximately the point/ordered
pair (5, 40). How do you actually do this? Also, how do you remove the
legend title (“class”)? Finally, how would you remove the plot legend
completely?

> the following demonstrates how to move the legend so it is
> approximately centered on the (5, 40) point on the plot, and how to
> remove the legend title. To remove the legend entirely, you could add
> `+ theme(legend.position = "none")`

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size = 2) + 
  theme(legend.direction = "horizontal") + 
  theme(legend.position = c(0.6, 0.85)) +
  theme(legend.title = element_blank())
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

### Graph Fail 4

I wanted just one smoothing line. Just one line, to show the general
relationship here. But that’s not happening. Instead I’m getting 3
lines, why and fix it please?

> you were getting 3 different lines because you specified to color by
> drv globally, so geom\_smooth was being divides up/colored by drv. You
> can fix this by coloring by drv for geom\_point only.

``` r
mpg %>% 
ggplot(mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = drv)) + 
  geom_smooth(se = F) #se = F makes it so it won't show the error in the line of fit
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph Fail 5

I got tired of the points, so I went to boxplots instead. However, I
wanted the boxes to be all one color, but setting the color aesthetic
just changed the outline? How can I make the box one color, not just the
outline?

> use fill instead of color :)

Also, the x-axis labels were overlaping, so I rotated them. But now they
overlap the bottom of the graph. How can I fix this so axis labels
aren’t on the graph?

> I solved this by playing with vjust.

``` r
ggplot(data = mpg, mapping = aes(x = manufacturer, y = cty, fill = manufacturer)) + 
  geom_boxplot() + 
  theme(axis.text.x = element_text(angle = 45, vjust=0.75))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

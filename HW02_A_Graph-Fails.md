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

``` r
data(mpg) #this is a dataset from the ggplot2 package

mpg %>% 
  ggplot(mapping = aes(x = city, y = hwy, color = "blue")) %>% 
  geom_point()
```

    ## Error: `mapping` must be created by `aes()`
    ## Did you use %>% instead of +?

### Corrected Graph 1

``` r
data(mpg) #this is a dataset from the ggplot2 package

  ggplot(mpg, aes(x = cty, y = hwy, color = "blue")) + 
  geom_point()
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Graph Fail 2

Why aren’t the points blue? It is making me blue that the points in the
graph aren’t blue :\`(

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

**The attribute *color = “blue”* is in the function aes(), so it is
treated as another aesthetic, or a variable, but it is supposed to be an
attribute.**

### Corrected Graph 2

``` r
ggplot(data = mpg) + 
  geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph Fail 3

Two mistakes in this graph. First, I wanted to make the the points
slightly bolder, but changing the alpha to 2 does nothing. What does
alpha do and what does setting it to 2 do? What could be done instead if
I want the points slightly bigger?

Second, I wanted to move the legend on top of the graph since there
aren’t any points there, putting it at approximately the point/ordered
pair (5, 40). How do you actually do this? Also, how do you remove the
legend title (“class”)? Finally, how would you remove the plot legend
completely?

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), alpha = 2) + 
  theme(legend.direction = "horizontal") + 
  theme(legend.position = c(5, 40))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

**The attribute *alpha* is a value between 0 and 1, and it sets opacity
of the point. Setting it to 2 is meaningless. You can set the attribute
*size* to make the point bigger.**

**We set position of legend by setting a point pair where values of x
and y are between 0 and 1, not following the text on the axis. Setting
*legend.title = element\_blank()* removes legend title, and setting
*legend.position = “none”* removes legend.**

### Corrected Graph 3 - Legend on the Top Without Title

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size = 2) + 
  theme(legend.direction = "horizontal") + 
  theme(legend.position = c(0.67, 0.86), legend.title = element_blank())
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

### Corrected Graph 3 - No Legend

``` r
mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size = 2) + 
  theme(legend.position = "none")
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

### Graph Fail 4

I wanted just one smoothing line. Just one line, to show the general
relationship here. But that’s not happening. Instead I’m getting 3
lines, why and fix it please?

``` r
mpg %>% 
ggplot(mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = F) #se = F makes it so it won't show the error in the line of fit
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

**“aes(color = drv)” was set after mapping, so that geometries in both
*point* and *smooth* layer were grouped according to *drv*. To solve
this problem, we can move “aes(color = drv)” to the point layer so that
there will be only one curve on the smooth layer.**

### Corrected Graph 4

``` r
mpg %>% 
ggplot(mapping = aes(x = displ, y = hwy)) + 
  geom_point(aes(color = drv)) + 
  geom_smooth(se = F) #se = F makes it so it won't show the error in the line of fit
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

### Graph Fail 5

I got tired of the points, so I went to boxplots instead. However, I
wanted the boxes to be all one color, but setting the color aesthetic
just changed the outline? How can I make the box one color, not just the
outline?

Also, the x-axis labels were overlaping, so I rotated them. But now they
overlap the bottom of the graph. How can I fix this so axis labels
aren’t on the graph?

``` r
ggplot(data = mpg, mapping = aes(x = manufacturer, y = cty, color = manufacturer)) + 
  geom_boxplot() + 
  theme(axis.text.x = element_text(angle = 45))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

**The aesthetic *color* is used to set color of the outline, while
*fill* is used for the inside.**

**We can adjust position of x axis labels by adding “vjust =”. Here
“vjust = 0.7” is sufficient.**

### Corrected Graph 5

``` r
ggplot(data = mpg, mapping = aes(x = manufacturer, y = cty, fill = manufacturer)) + 
  geom_boxplot() + 
  theme(axis.text.x = element_text(angle = 45, vjust = 0.7))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

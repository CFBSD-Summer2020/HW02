What went wrong?
================
ALthea Bock-Hughes

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
  ggplot(mapping = aes(x = cty, y = hwy, color = "blue")) +
  geom_point()
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
#I changed "city" to "cty" and changed the pipeline symbol to a "+" 
```

### Graph Fail 2

Why aren’t the points blue? It is making me blue that the points in the
graph aren’t blue
:\`(

``` r
ggplot(mpg, aes(x = displ, y = hwy)) + geom_point(color = "blue")
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

``` r
#I moved the "color=blue" to the point layer so that it was an attribute not an aesthetic
```

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
Figure3 <- mpg %>% 
ggplot() + 
  geom_point(mapping = aes(x = displ, y = hwy, color = class), size=3) 

#Alpha refers to the transperancy of the dot, so I changed it to "size' and placed it outside of the aesthetic to make it an atribute 

#this is the graph with the legend (I took off your theme layers)
Figure3 
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
#this is the graph with the legend in the top right corner (the coordinates have to be 0-1), and you have to make the key smaller so the data isn't covered 
Figure3 + theme(legend.key.size = unit(.75, "lines"), legend.justification=c(1,1), legend.position=c(1,1))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-2.png)<!-- -->

``` r
#This is how you remove a legend title
Figure3 + theme(legend.title = element_blank())
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-3.png)<!-- -->

``` r
#this removes all legends
Figure3 + theme(legend.position = "none")
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-3-4.png)<!-- -->

### Graph Fail 4

I wanted just one smoothing line. Just one line, to show the general
relationship here. But that’s not happening. Instead I’m getting 3
lines, why and fix it please?

``` r
#you need to put the color aesthetic in the point layer
mpg %>% 
ggplot(mapping = aes(x = displ, y = hwy)) + 
  geom_point(aes(color = drv)) + 
  geom_smooth(se = F) #se = F makes it so it won't show the error in the line of fit
```

    ## `geom_smooth()` using method = 'loess' and formula 'y ~ x'

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph Fail 5

I got tired of the points, so I went to boxplots instead. However, I
wanted the boxes to be all one color, but setting the color aesthetic
just changed the outline? How can I make the box one color, not just the
outline?

Also, the x-axis labels were overlaping, so I rotated them. But now they
overlap the bottom of the graph. How can I fix this so axis labels
aren’t on the graph?

``` r
#You can changed the aesthetic to "fill" if you really want
ggplot(mpg, aes(x = manufacturer, y = cty, fill = manufacturer)) + 
  geom_boxplot() + 
  theme(axis.text.x = element_text(angle = 45))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
#setting the manufacturer to an aesthetic twice doesn't seem nesseccary so I'm making all the boxes the same color in atributes 

ggplot(mpg, aes(x = manufacturer, y = cty)) + 
  geom_boxplot(fill="purple") + 
  theme(axis.text.x = element_text(angle = 45))
```

![](HW02_A_Graph-Fails_files/figure-gfm/unnamed-chunk-5-2.png)<!-- -->

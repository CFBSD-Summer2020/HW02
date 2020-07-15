HW02\_B\_Graph-Mimic
================
Robert Gruener

``` r
library("ggplot2")
library("magrittr") #so I can do some piping
data("diamonds")
data("mpg")
data("iris")
theme_set(theme_bw()) #I'll give you this one, you can set the theme individually for graphs
#or you can set the theme for all the graphs using theme_set()
#theme_bw() is best theme (IMO)

#for graph 3:
library("ggrepel")
```

## HW02 Part B

For this part of the HW, the goal is to try to recreate the graphs I
make from scratch. I will only provide the MD, not the actual code I
used to create it besides which data I use to create it. The rest will
be up to you.

Try for all 4, but if you are struggling don’t worry about it. Try your
best for each, if you don’t get everything that’s what the peer-review
is for. :smile:

### Graph 1

``` r
data("diamonds")
#hint think about the *position* the bars are in...

ggplot(diamonds, aes(x = cut, fill = clarity)) +
  geom_bar(position = "dodge") +
  labs(title = "My Diamond Collection", subtitle = "Boxplot representing the number of diamonds in my diamond collection by type of cut quality and clarity of diamond", x = "Diamond Cut", y = "Number of Diamonds") +
  annotate(
    "text",
    x = 4, y = 5000,
    label = "My Best Diamonds, of course",
    vjust = 1, size = 3
  )
  
```

Using the diamonds dataset, make this graph:
![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

### Graph 2

``` r
data("iris")
```

Using the iris dataset, make this graph:

    ## `geom_smooth()` using formula 'y ~ x'
    
ggplot(iris, aes(Sepal.Length, Petal.Length)) +
  geom_point(aes(shape = factor(Species), color = factor(Species))) +
  facet_wrap("Species") +
  geom_smooth(formula = y ~ x)

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph 3

You’ll need the information in this first box to create the graph

``` r
data("mpg")
corvette <- mpg[mpg$model == "corvette",]
#install
require("ggrepel") #useful for making text annotations better, hint hint
set.seed(42)
```

Now using the mpg dataset and the corvette dataset, make this graph:

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

There is a trick to getting the model and year to print off together.
`paste()` is a useful function for this, also pasting together parts of
file names and parts of urls together.

ggplot(mpg, aes(displ, hwy)) +
  geom_point() +
  geom_point(data = corvette, color = "red") +
  geom_text(data = corvette, aes(label = paste(model, year), hjust = 1.1)) +
  labs(title = "Corvettes are a bit of an outlier")

### Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options
```

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

The above graph lets you see some colobrlind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

ggplot(mpg, aes(class, cty, color = class)) +
  geom_boxplot() +
  geom_jitter() +
  coord_flip() +
  scale_color_brewer(palette="Set2") +
  labs(title = "Horizontal Boxplot of City MPG and Car Class", y = "City MPG", x = "Car Class")


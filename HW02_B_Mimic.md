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
  #1D plot, position is side-to-side
  geom_bar(position = "dodge") +
  #Adding in rectangle shape
  annotate("rect", xmin = 4.5, xmax = 5.5, ymin = 0, ymax = 5000, alpha = 0.4) +
  #Adding in a text box
  annotate("text", x = 4, y = 4500, label = "My Best Diamonds, \nof course") +
  #Adding all of the labels
  labs(x="Diamond Cut", y= "Number of Diamonds", title = "My Diamond Collection", subtitle = "Boxplot representing the number of diamonds in my diamond collection by type of cut and clarity of diamond")

```

### Graph 2

``` r
data("iris")

ggplot(iris, aes(x = Sepal.Length, y = Petal.Length, shape = Species, color = Species)) +
  geom_point() +
  geom_smooth(method = "lm", color = "black", se = F, formula = y~x)


```

Using the iris dataset, make this graph:

    ## `geom_smooth()` using formula 'y ~ x'

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph 3

You’ll need the information in this first box to create the graph

``` r
data("mpg")
corvette <- mpg[mpg$model == "corvette",]
#install
require("ggrepel") #useful for making text annotations better, hint hint
set.seed(42)

ggplot(mpg, aes(x = displ, y = hwy)) +
  geom_point() +
  geom_point(corvette, color = "blue") +
  labs(subtitle = "Corvettes are a bit of an outlier")

```

Now using the mpg dataset and the corvette dataset, make this graph:

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

There is a trick to getting the model and year to print off together.
`paste()` is a useful function for this, also pasting together parts of
file names and parts of urls together.

### Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options

data(mpg)
ggplot(mpg, aes(x = class,y = cty, color = class)) +
  labs(x = "Car Class", y = "City mpg", title = "Horizontal BoxPlot of City MPG and Car Class") +
  geom_boxplot(color = "black") +
  geom_point() +
  geom_jitter() 
  

```

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

The above graph lets you see some colobrlind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

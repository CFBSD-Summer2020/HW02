HW02\_B\_Graph-Mimic
================
Ricardo Muñiz Trejo

``` r
library("ggplot2")
```

    ## Warning: package 'ggplot2' was built under R version 4.0.2

``` r
library("magrittr") #so I can do some piping
```

    ## Warning: package 'magrittr' was built under R version 4.0.2

``` r
data("diamonds")
data("mpg")
data("iris")
theme_set(theme_bw()) #I'll give you this one, you can set the theme individually for graphs
#or you can set the theme for all the graphs using theme_set()
#theme_bw() is best theme (IMO)

#for graph 3:
library("ggrepel")
```

    ## Warning: package 'ggrepel' was built under R version 4.0.2

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
```

Using the diamonds dataset, make this graph:

``` r
ggplot(diamonds, aes(cut, fill = clarity)) +
  geom_bar(position = "dodge") +
  #To add labels to title, subtitle, x- and y-axes.
  labs(title = "My Diamond Collection", 
       subtitle = "Boxplot representing the number of diamonds in my  diamond collection by \ntype of cut quality and clarity of diamond",
       x = "Diamond Cut", 
       y = "Number of Diamonds") +
  theme(plot.title = element_text(hjust = 0.5)) +
  #annotate() to add the text and the rectangle
  annotate("text", x = 4, y = 4500, 
           label = "My Best Diamonds,\nof course") +
  annotate("rect", xmin = 4.5, xmax = 5.5, 
           ymin = 0, ymax = 5000, 
           alpha = 0.3)
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph1%20code-1.png)<!-- -->

### Graph 2

``` r
data("iris")
```

Using the iris dataset, make this graph:

``` r
#To reorder the panels within the graph
iris$Species2 <- factor(iris$Species, levels = c("versicolor", "setosa", "virginica"))

ggplot(iris, aes(Sepal.Length, Petal.Length, color = Species, shape = Species))+
  geom_point() +
  geom_smooth(se = F, method = lm, color = "black") +
  #To put species in different panels
  facet_wrap(vars(Species2), scales = "free") +
  #To resize x-axis per species
  scale_x_continuous(limits = c(4.25,8))
```

    ## `geom_smooth()` using formula 'y ~ x'

![](HW02_B_Mimic_starter_files/figure-gfm/graph%202%20code-1.png)<!-- -->

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

``` r
#Define the label you want to add with paste() as an aesthetic
ggplot(mpg, aes(displ,hwy, label = paste("Corvette", year, sep = ","))) +
  #To label use the ggrepel package
  geom_text_repel(
    data = corvette,
    segment.size = 0.2,
    segment.color = "black",
    nudge_x = 0.4
  ) +
  #To only color the points for Corvette models
  geom_point(color = ifelse(mpg$model == "corvette", "blue", "black")) +
  labs(title = "Corvettes are a bit of an outlier") +
  scale_x_continuous(limits = c(1,7.9), breaks = seq(1:8))
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%203%20code-1.png)<!-- -->

There is a trick to getting the model and year to print off together.
`paste()` is a useful function for this, also pasting together parts of
file names and parts of urls together.

### Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options
```

![](HW02_B_Mimic_starter_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

The above graph lets you see some colorblind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

``` r
ggplot(mpg, aes(cty, class)) +
  geom_boxplot(outlier.shape = NA) +
  geom_jitter(aes(color = class), width = 0, height = 0.4) +
  labs(title = "Horizontal BoxPlot of City MPG and Car Class",
       x = "Car Class",
       y = "City MPG") +
   #Colorblind friendly palette "Set2"
  scale_color_brewer(palette = "Set2")
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%204%20code-1.png)<!-- -->

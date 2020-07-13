HW02\_B\_Graph-Mimic
================
Patrick Haller

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

### Here is my attempt to recreate Graph 1

``` r
data("diamonds")
#hint think about the *position* the bars are in...
```

``` r
ggplot(diamonds, aes(x = cut, fill = clarity)) +
  geom_bar(position = "dodge") + 
  labs(x = "Diamond Cut", y = "Number of Diamonds", title = "My Diamond Collection", subtitle = "Boxplot representing the number of diamonds in my diamond collection by \ntype of cut quality and clarity of diamond") + 
  theme(plot.title = element_text(hjust = 0.5)) + 
  annotate("text", x = 4, y = 4500, label = "My Best Diamonds,\nof course") +
  annotate("rect", xmin = 4.5, xmax = 5.5, ymin = 0, ymax = 5000, alpha = 0.3)
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph1%20code-1.png)<!-- -->

### Here is my attempt to recreate Graph 2

``` r
data("iris")
```

``` r
ggplot(iris, aes(Sepal.Length, Petal.Length)) +
  geom_point(aes(shape = Species, color = Species)) + 
  facet_wrap(~ Species, scales = "free_y") +
  geom_smooth(method = "lm", se = F, color = "black")
```

    ## `geom_smooth()` using formula 'y ~ x'

![](HW02_B_Mimic_starter_files/figure-gfm/graph%202%20code-1.png)<!-- -->

``` r
#is there a way to move the setosa panel to the middle and versicolor to the left?
```

### Here is my attempt to recreate Graph 3

``` r
data("mpg")
corvette <- mpg[mpg$model == "corvette",]
#install
require("ggrepel") #useful for making text annotations better, hint hint
set.seed(42)
```

``` r
ggplot(mpg, aes(displ, hwy)) +
  geom_point(size = 1) + 
  geom_point(data = corvette, aes(displ, hwy), color = "blue", size = 1) +
  geom_text_repel(data = corvette, aes(label = paste("Corvette,",year))) +
  labs(title = "Corvettes are a bit of an outlier") + 
  scale_x_continuous(breaks = seq(1, 8, by = 1), limits = c(1, 8)) 
```

![](HW02_B_Mimic_starter_files/figure-gfm/graoh%203%20code-1.png)<!-- -->

There is a trick to getting the model and year to print off together.
`paste()` is a useful function for this, also pasting together parts of
file names and parts of urls together.

### Here is my attempt to recreate Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options
```

![](HW02_B_Mimic_starter_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

``` r
ggplot(data = mpg, mapping = aes(cty, class)) +
  geom_jitter(mapping = aes(color = class), size = 1, width = 0) +
  scale_color_brewer(palette = "Set2") +
  geom_boxplot(alpha = 0) +
  labs(title = "Horizontal BoxPlot of City MPG and Car Class", x = "Car Class", y = "City mpg") +
  theme(panel.grid.major = element_blank(), panel.grid.minor = element_blank(), panel.background = element_blank(), panel.border = element_blank(), axis.line = element_line(color = "black"))
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%204%20code-1.png)<!-- -->

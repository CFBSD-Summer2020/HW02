HW02\_B\_Graph-Mimic
================
Mingyu Qi

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
```

Using the diamonds dataset, make this graph:

``` r
ggplot(diamonds,aes(cut, fill=clarity)) + 
#Make bars dodged side-to-side
geom_bar(position="dodge") + 
#Create labels for x-axis, y-axis, title, and subtitle
labs(x="Diamond Cut", y="Number of Diamonds", title="My Diamond Collection", subtitle="Boxplot representing the number of diamonds in my diamond collection by \n type of cut quality and clarity of diamond") +
#Create a rectangle annotate
annotate("rect", xmin = 4.5, xmax = 5.5, ymin=0, ymax = 5000, alpha=0.3) +
#Add text annotate (use \n to change to the next line)
annotate("text", x=4, y=4500, label="My Best Diamonds, \n of course") +
#Center the title 
theme(plot.title = element_text(hjust = 0.5)) 
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph1%20code-1.png)<!-- -->

### Graph 2

``` r
data("iris")
```

Using the iris dataset, make this graph:

``` r
#Re-order the values of Species 
iris$Species <- factor(iris$Species,levels=c("versicolor","setosa","virginica"))
ggplot(iris,aes(Sepal.Length, Petal.Length, shape=Species, color=Species)) + 
geom_point() +
#Add a regression line in each graph
geom_smooth(method = "lm", formula = y ~ x, color="black", size=1.25, se=FALSE, span=1) + 
#Wrapping with Species and make independent axis scales for each graph 
facet_wrap(. ~ Species, scales="free_y") + 
scale_color_manual(values = c('#00ba38','#f87676', '#619bff')) +
scale_shape_manual(values=c(17,16,15)) 
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%202%20code-1.png)<!-- -->

``` r
#How to re-order the items in legend? 
```

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
ggplot(mpg, aes(displ,hwy)) + 
geom_point() + 
geom_text_repel(aes(displ,hwy,label=paste("Corvette", year, sep=",")), corvette) +
geom_point(aes(displ,hwy), corvette, color="blue") +
labs(title="Corvette are a bit of an outlier") + 
scale_x_continuous(breaks=c(1:8), limits=c(1,8))
```

![](HW02_B_Mimic_starter_files/figure-gfm/graoh%203%20code-1.png)<!-- -->

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

The above graph lets you see some colobrlind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

``` r
ggplot(mpg,aes(cty,class,color=class)) + 
#Turn off the shape of outlying point
geom_boxplot(color="black", outlier.shape=NA) + 
geom_jitter(width=0,height=0.4) +
scale_color_brewer(palette="Set2") +
#I think the x-axis should be labeled as "City mpg" and y-axis should be labeled as "Car Class"
labs(x="City mpg", y="Car Class", title="Horizontal Box Plot of City MPG and Car Class") + 
theme(axis.line=element_line(color="black"), panel.grid.major=element_blank(), panel.grid.minor= element_blank(), panel.background=element_blank(), panel.border=element_blank()) 
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%204%20code-1.png)<!-- -->

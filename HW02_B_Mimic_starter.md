HW02\_B\_Graph-Mimic
================
Alex Hoover

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
ggplot(data=diamonds, mapping=aes(x=cut, fill=clarity))+ geom_bar(position="dodge")+labs(y="Number of Diamonds", x="Diamond Cut", title="My Diamond Collection", subtitle= "Boxplot representing the number of diamonds in my diamond collection by \n type of cut quality and clarity of diamond")+theme(plot.title=element_text(hjust=0.5))+annotate("rect", xmin=4.5, xmax=5.5, ymin=0, ymax=5000, alpha=0.2)+annotate("text", x=4, y=4500,label="My Best Diamonds,\n of course")
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph1%20code-1.png)<!-- -->

### Graph 2

Using the iris dataset, make this graph:

``` r
data("iris")
ggplot(data=iris, mapping=aes(x=Sepal.Length, y=Petal.Length,group=Species))+geom_point(aes(shape=Species, color=Species))+facet_wrap(~Species,scales='free_y')+geom_smooth(method='lm', color="black", se=FALSE)
```

    ## `geom_smooth()` using formula 'y ~ x'

![](HW02_B_Mimic_starter_files/figure-gfm/graph%202%20code-1.png)<!-- -->
Not sure how to change the order of the graphs.

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
ggplot(data=mpg, mapping=aes(x=displ, y=hwy,))+geom_point()+labs(title="Corvettes are a bit of an outlier")+geom_text_repel(data = corvette, label = paste("Corvette,", corvette$year))+geom_point(data=corvette, color="blue")
```

![](HW02_B_Mimic_starter_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Graph 4

``` r
data(mpg)

#hint for the coloring, colorbrewer and you can set palette colors and make your graphs colorblind friendly
library(RColorBrewer)
display.brewer.all(colorblindFriendly = T) #take a look at the colorblindfriendly options
```

![](HW02_B_Mimic_starter_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

The above graph lets you see some colobrlind friendly palettes. For the
graph below, I used Set2.

Now using the above mpg dataset, make this graph

``` r
ggplot(data=mpg, mapping=aes(x=cty, y=class, color=class))+geom_boxplot(color="black",show.legend=FALSE)+geom_point()+geom_jitter()+scale_color_brewer(palette="Set2")+labs(title="Horizontal BoxPlot of City MPG and Car Class", x= "City MPG", y= "Car Class")+theme(panel.grid.major=element_blank(), panel.grid.minor=element_blank(), panel.border=element_blank(), axis.line=element_line(color="black"))
```

![](HW02_B_Mimic_starter_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

Not sure how to set the x-axis tick lines by counts of 5.

### Original Graphs

![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-2-1.png)
![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-4-1.png)
![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-6-1.png)
![](HW02_B_Mimic_files/figure-gfm/unnamed-chunk-8-1.png)

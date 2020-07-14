HW02\_B\_Graph-Mimic
================
YOUR NAME HERE

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

    ## Warning: package 'ggrepel' was built under R version 4.0.1

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
ggplot(data=diamonds,mapping= aes(x=cut, fill=clarity))+
  geom_rect(xmin = 4.5,xmax=5.5,ymin=0, ymax=5000, fill = "grey", alpha = 0.1)+
  geom_histogram(stat="count", position = "dodge2")+
   ggtitle ("My Diamond Collection", subtitle="Boxplot representing the number of diamonds in my diamond collection by \ntype of cut quality and clarity of diamond")+
  xlab("Diamond Cut")+
  ylab("Number of Diamonds")+
  theme(plot.title = element_text(hjust = 0.5))+
  annotate("text",x=4, y=4500, label="My Best Diamonds, \nof course")
```

    ## Warning: Ignoring unknown parameters: binwidth, bins, pad

![](HW02_B_Mimic_starter_files/figure-gfm/graph1%20code-1.png)<!-- -->

### Graph 2

``` r
data("iris")
```

Using the iris dataset, make this
graph:

``` r
ggplot(data=iris, aes(x= Sepal.Length, y=Petal.Length, color=Species, shape=Species) )+
  geom_point()+
  geom_smooth(method="lm",color="black")+
  facet_grid(.~Species,scales = "free", space="free")
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
#corvette is a subset of mpg. dot plot (x=displ, y=hwy)
ggplot(data = mpg,mapping= aes(x=displ, y=hwy,label=model))+
  geom_point(color=ifelse(mpg$model=="corvette", "blue","black"))+
  geom_text_repel( 
    data=corvette, mapping= aes(label= paste(model, "," ,year), inherit.aes=F)
  )
```

    ## Warning: Ignoring unknown aesthetics: inherit.aes

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
ggplot(data = mpg,mapping= aes(x=class, y=cty,color=class))+
    #geom_dotplot(aes(x=as.numeric(class), group=class))+
    geom_boxplot()
```

![](HW02_B_Mimic_starter_files/figure-gfm/graph%204%20code-1.png)<!-- -->

# HW02
Due 7/13/2020

There are two parts to the HW this week. 

[The first assignment asks you to fix some common issues with making ggplot plots ](HW02_A_Graph-Fails.Rmd). You can find the code in that link or the file: HW02_A_Graph-Fails.Rmd

### Graph Fail 1
The error was to use + instead of %<%. Also, the city object was not found and as Highway is abbreviated as hwy, city should have been abbreviated to cty. Below is the corrected code.

### Graph Fail 2
The color attribute needed to be kept outside the `aes()` function

### Graph Fail 3
Alpha determines the opacity of the point. Size function is required for the bolder points.

Legend.position at (0,0) represent bottom left and (1,1) represent top right and so, to move the legend on top empty space of the graph, we can assign (0.70, 0.90). The legend title can be removed by using element_blank() function. To remove the legend completely, we could add theme(legend.position = none)

### Graph Fail 4
color= drv aesthetic was assigned into `aes` function and hence three different lines .

As we plan to map only x and y aesthetics, the color has to be kept seperately outside the `aes()` function. Assigning "black" color function to geom_smooth method brings only one oliud line connecting all points. 

### Graph Fail 5
In case of assigning the same color to all boxes, we use the function "fill" instead of "color".

vertical justification (vjust) tool allows to modify the distance between the X-axis label and x-axis ticks.



The second part of the HW will likely be more challenging as it asks you to try to recreate the graphs from just the images. [Here is a link to the markdown file](HW02_B_Mimic.md) with the images you will try to recreate or you can just find the file "HW02_B_Mimic.md" or find the html version "HW02_B_Mimic.html" (which would need to be previewed in RStudio or opened up by an internet browser to view properlY) in the repo. To make your lives easier, I also created a "starter" document that has the same code that you can find in the markdown (but obviously the code for the graphs themselves was removed). [Here is a link to the starter document](HW02_B_Mimic_starter.Rmd) or you can look for the file "HW02_B_Mimic_starter.Rmd" 


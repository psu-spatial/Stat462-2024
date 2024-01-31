

# Plots

Plots are designed to do two things, allow you to see something in the data that you couldn't see in the numbers, plus communicate output in a compelling way.

Going beyond the basics or knowing the limitations of a plot will help you do this, so in these examples I have provided a range of complexity. You will see tutorials for all the plots I mention in this section. If in doubt, try the ggstatsplot versions.

<br>

### What to choose?

-   If you are looking at a single variable, try histograms, boxplots and violin plots

-   If you think your histogram changes by some category, try grouped boxplots and grouped violin plots (easy violin plot here)

-   If you think your histogram changes numerically, try ridgeline plots

-   If you are comparing two variables, try scatterplots and correlation plots.

<br>

### Where to find worked examples

There are three places I visit constantly:

-   <https://www.r-graph-gallery.com/>
-   <https://indrajeetpatil.github.io/ggstatsplot/>
-   <https://r-charts.com/distribution/>
-   <https://flowingdata.com/>

For plots, we have *many* choices. We can use what is built into R, or.. use the ggplot system where you add on layers to your plot using the + symbol, or use specialist packages such as ggstatplot or beeswarm.

If you are new to data visualisation, read these two articles

-   <https://flowingdata.com/2014/10/23/moving-past-default-charts/>
-   <https://flowingdata.com/2012/05/15/how-to-visualize-and-compare-distributions/>

<br>

## Plot gallery


<br> <br>

### Scatterplots

#### Built in plot command

Here is the absolute basic scatterplot.  This should not be the one you submit in your reports (e.g. either choose a more professional one or adjust the options below)


```r
# you can either do plot(x, y)
# OR (recommended), use the ~ to say plot(y~x) 
# e.g. y depends on x

HousesNY$Beds <- as.numeric(HousesNY$Beds)

plot(HousesNY$Price ~ HousesNY$Beds)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-1-1.png" width="672" />

See below for how to add a line of best fit.

There are many things we can change, see the help file for the `par` command for more.

For example, here is an ugly plot showing as many as I can think!


```r
plot(HousesNY$Price ~ HousesNY$Beds,
     xlim=c(0,7), #xlimits
     ylim=c(40,220), #ylimits
     xlab=list("Beds",cex=.8,col="red",font=2), # play with x-label
     ylab=list("Price",cex=1.2,col="blue",font=3), # play with x-label
     main="Ugly feature plot",
     cex=1.2, #point size
     pch=16, # symbol shape (try plot(1:24,1:24,pch=1:24 to see them all))
     tcl=-.25, # smaller tick marks
     mgp=c(1.75,.5,0)) # move the x/y labels around

grid() #  add a grid

# lines means "add points on top"
lines(HousesNY$Price ~ HousesNY$Beds, 
     type="p", # p for points, "l" for lines, "o" for both, "h for bars
     xlim=c(0,7), #xlimits
     ylim=c(40,220), #ylimits
     col="yellow",
     cex=.5, #point size
     pch=4) # move the x/y labels around
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-2-1.png" width="672" />


#### adding a lione of best fit

To add a line, you can use the abline command IN THE SAME CODE CHUNK. For example


```r
plot(HousesNY$Price ~ HousesNY$Beds,
     xlim=c(0,7), #xlimits
     ylim=c(40,220), #ylimits
     xlab=list("Beds",cex=.8,col="red",font=2), # play with x-label
     ylab=list("Price",cex=1.2,col="blue",font=3), # play with x-label
     main="", # no title
     cex=1.2, #point size
     pch=16, # symbol shape (try plot(1:24,1:24,pch=1:24 to see them all))
     tcl=-.25, # smaller tick marks
     mgp=c(1.75,.5,0)) # move the x/y labels around

# add vertical line at 3.5
abline(v=5.5,col="red")
# add horizontal line at the mean of price
abline(h=mean(HousesNY$Price)) 
# add line of best fit
abline(lm(HousesNY$Price ~ HousesNY$Beds),col="blue",lty="dotted",lwd=3) 
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-3-1.png" width="672" />

#### ggplot


GGPlot also has basic and advanced options, but you need to install/run the ggplot2 package. From the basics:


```r
library(ggplot2)
#
ggplot(HousesNY, aes(x=Beds, y=Price)) + 
    geom_point()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-4-1.png" width="672" />

To more advanced:


```r
library(ggplot2)
library(hrbrthemes)

# use options!
ggplot(HousesNY, aes(x=Beds, y=Price)) + 
    geom_point(
        color="black",
        fill="#69b3a2",
        shape=22,
        alpha=0.5,
        size=6,
        stroke = 1
        ) +
    theme_ipsum()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-5-1.png" width="672" />

Adding a line of best fit is also easy, but fits less easily with R's modelling commands:


```r
# Library
library(ggplot2)
library(hrbrthemes)

# Create dummy data
data <- data.frame(
  cond = rep(c("condition_1", "condition_2"), each=10), 
  my_x = 1:100 + rnorm(100,sd=9), 
  my_y = 1:100 + rnorm(100,sd=16) 
)

# Basic scatter plot.
p1 <- ggplot(data, aes(x=my_x, y=my_y)) + 
  geom_point( color="#69b3a2") +
  theme_ipsum()
 
# with linear trend
p2 <- ggplot(data, aes(x=my_x, y=my_y)) +
  geom_point() +
  geom_smooth(method=lm , color="red", se=FALSE) +
  theme_ipsum()

# linear trend + confidence interval
p3 <- ggplot(data, aes(x=my_x, y=my_y)) +
  geom_point() +
  geom_smooth(method=lm , color="red", fill="#69b3a2", se=TRUE) +
  theme_ipsum()

p1
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```r
p2
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-6-2.png" width="672" />

```r
p3
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-6-3.png" width="672" />

#### Interactive!


Or using the plotly library to make your plots interactive (really useful, try zooming in or clicking on a few points)


```r
# create the plot, save it as "p" rather than print immediately
myplot <-   ggplot(HousesNY, aes(x=Beds, y=Price, label=Baths)) + 
            geom_point(alpha=.5) +
            theme_classic()
            
# and plot interactively
ggplotly(myplot)
```

```{=html}
<div class="plotly html-widget html-fill-item" id="htmlwidget-551216ac6fc05ae82cd4" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-551216ac6fc05ae82cd4">{"x":{"data":[{"x":[3,6,4,3,3,2,2,4,4,3,3,3,3,4,3,3,4,3,4,3,4,4,5,4,3,2,3,3,4,3,3,3,3,3,3,2,3,3,3,4,2,4,4,4,4,3,4,3,4,4,5,4,3],"y":[57.600000000000001,120,150,143,92.5,50,89,140,197.5,125.09999999999999,175,60,138.5,160,63.5,107,185,82.700000000000003,75,118,87.5,67.5,105,114,100.5,78,99,144,179,110,175,100,53,92,127,120.5,72,95,38.5,139,75,174,119,89,75.099999999999994,92.5,141,82,162,195,190,115,87],"text":["Beds: 3<br />Price:  57.6<br />Baths: 2.0","Beds: 6<br />Price: 120.0<br />Baths: 2.0","Beds: 4<br />Price: 150.0<br />Baths: 2.0","Beds: 3<br />Price: 143.0<br />Baths: 2.0","Beds: 3<br />Price:  92.5<br />Baths: 1.0","Beds: 2<br />Price:  50.0<br />Baths: 1.0","Beds: 2<br />Price:  89.0<br />Baths: 2.0","Beds: 4<br />Price: 140.0<br />Baths: 3.0","Beds: 4<br />Price: 197.5<br />Baths: 2.5","Beds: 3<br />Price: 125.1<br />Baths: 2.0","Beds: 3<br />Price: 175.0<br />Baths: 2.0","Beds: 3<br />Price:  60.0<br />Baths: 1.0","Beds: 3<br />Price: 138.5<br />Baths: 2.0","Beds: 4<br />Price: 160.0<br />Baths: 2.0","Beds: 3<br />Price:  63.5<br />Baths: 2.0","Beds: 3<br />Price: 107.0<br />Baths: 1.0","Beds: 4<br />Price: 185.0<br />Baths: 3.5","Beds: 3<br />Price:  82.7<br />Baths: 1.0","Beds: 4<br />Price:  75.0<br />Baths: 2.0","Beds: 3<br />Price: 118.0<br />Baths: 1.0","Beds: 4<br />Price:  87.5<br />Baths: 2.0","Beds: 4<br />Price:  67.5<br />Baths: 1.0","Beds: 5<br />Price: 105.0<br />Baths: 2.0","Beds: 4<br />Price: 114.0<br />Baths: 2.0","Beds: 3<br />Price: 100.5<br />Baths: 2.0","Beds: 2<br />Price:  78.0<br />Baths: 1.0","Beds: 3<br />Price:  99.0<br />Baths: 1.0","Beds: 3<br />Price: 144.0<br />Baths: 1.5","Beds: 4<br />Price: 179.0<br />Baths: 2.0","Beds: 3<br />Price: 110.0<br />Baths: 1.5","Beds: 3<br />Price: 175.0<br />Baths: 2.0","Beds: 3<br />Price: 100.0<br />Baths: 2.0","Beds: 3<br />Price:  53.0<br />Baths: 1.0","Beds: 3<br />Price:  92.0<br />Baths: 2.0","Beds: 3<br />Price: 127.0<br />Baths: 2.0","Beds: 2<br />Price: 120.5<br />Baths: 2.0","Beds: 3<br />Price:  72.0<br />Baths: 2.0","Beds: 3<br />Price:  95.0<br />Baths: 2.0","Beds: 3<br />Price:  38.5<br />Baths: 1.0","Beds: 4<br />Price: 139.0<br />Baths: 2.0","Beds: 2<br />Price:  75.0<br />Baths: 2.0","Beds: 4<br />Price: 174.0<br />Baths: 3.0","Beds: 4<br />Price: 119.0<br />Baths: 2.0","Beds: 4<br />Price:  89.0<br />Baths: 1.0","Beds: 4<br />Price:  75.1<br />Baths: 2.0","Beds: 3<br />Price:  92.5<br />Baths: 2.0","Beds: 4<br />Price: 141.0<br />Baths: 1.0","Beds: 3<br />Price:  82.0<br />Baths: 3.0","Beds: 4<br />Price: 162.0<br />Baths: 1.5","Beds: 4<br />Price: 195.0<br />Baths: 3.0","Beds: 5<br />Price: 190.0<br />Baths: 3.5","Beds: 4<br />Price: 115.0<br />Baths: 2.0","Beds: 3<br />Price:  87.0<br />Baths: 1.5"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,0,0,1)","opacity":0.5,"size":5.6692913385826778,"symbol":"circle","line":{"width":1.8897637795275593,"color":"rgba(0,0,0,1)"}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":26.228310502283108,"r":7.3059360730593621,"b":40.182648401826498,"l":43.105022831050235},"plot_bgcolor":"rgba(255,255,255,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1.8,6.2000000000000002],"tickmode":"array","ticktext":["2","3","4","5","6"],"tickvals":[2,3,4,5,6],"categoryorder":"array","categoryarray":["2","3","4","5","6"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176002,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"Beds","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[30.550000000000001,205.44999999999999],"tickmode":"array","ticktext":["50","100","150","200"],"tickvals":[50,100,150,200],"categoryorder":"array","categoryarray":["50","100","150","200"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176002,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"x","title":{"text":"Price","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.8897637795275593,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.68949771689498}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"12fb561a7bb21":{"x":{},"y":{},"label":{},"type":"scatter"}},"cur_data":"12fb561a7bb21","visdat":{"12fb561a7bb21":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

It's also very easy to add in color to see another variable. For example


```r
# create the plot, save it as "p" rather than print immediately
myplot <-   ggplot(HousesNY, aes(x=Beds, y=Price,color=Baths)) + 
            geom_point(alpha=.5) +
            theme_classic()+
            scale_color_gradient(low="blue", high="red")

# and plot interactively
ggplotly(myplot)
```

```{=html}
<div class="plotly html-widget html-fill-item" id="htmlwidget-abe055109619f0b9d56a" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-abe055109619f0b9d56a">{"x":{"data":[{"x":[3,6,4,3,3,2,2,4,4,3,3,3,3,4,3,3,4,3,4,3,4,4,5,4,3,2,3,3,4,3,3,3,3,3,3,2,3,3,3,4,2,4,4,4,4,3,4,3,4,4,5,4,3],"y":[57.600000000000001,120,150,143,92.5,50,89,140,197.5,125.09999999999999,175,60,138.5,160,63.5,107,185,82.700000000000003,75,118,87.5,67.5,105,114,100.5,78,99,144,179,110,175,100,53,92,127,120.5,72,95,38.5,139,75,174,119,89,75.099999999999994,92.5,141,82,162,195,190,115,87],"text":["Beds: 3<br />Price:  57.6<br />Baths: 2.0","Beds: 6<br />Price: 120.0<br />Baths: 2.0","Beds: 4<br />Price: 150.0<br />Baths: 2.0","Beds: 3<br />Price: 143.0<br />Baths: 2.0","Beds: 3<br />Price:  92.5<br />Baths: 1.0","Beds: 2<br />Price:  50.0<br />Baths: 1.0","Beds: 2<br />Price:  89.0<br />Baths: 2.0","Beds: 4<br />Price: 140.0<br />Baths: 3.0","Beds: 4<br />Price: 197.5<br />Baths: 2.5","Beds: 3<br />Price: 125.1<br />Baths: 2.0","Beds: 3<br />Price: 175.0<br />Baths: 2.0","Beds: 3<br />Price:  60.0<br />Baths: 1.0","Beds: 3<br />Price: 138.5<br />Baths: 2.0","Beds: 4<br />Price: 160.0<br />Baths: 2.0","Beds: 3<br />Price:  63.5<br />Baths: 2.0","Beds: 3<br />Price: 107.0<br />Baths: 1.0","Beds: 4<br />Price: 185.0<br />Baths: 3.5","Beds: 3<br />Price:  82.7<br />Baths: 1.0","Beds: 4<br />Price:  75.0<br />Baths: 2.0","Beds: 3<br />Price: 118.0<br />Baths: 1.0","Beds: 4<br />Price:  87.5<br />Baths: 2.0","Beds: 4<br />Price:  67.5<br />Baths: 1.0","Beds: 5<br />Price: 105.0<br />Baths: 2.0","Beds: 4<br />Price: 114.0<br />Baths: 2.0","Beds: 3<br />Price: 100.5<br />Baths: 2.0","Beds: 2<br />Price:  78.0<br />Baths: 1.0","Beds: 3<br />Price:  99.0<br />Baths: 1.0","Beds: 3<br />Price: 144.0<br />Baths: 1.5","Beds: 4<br />Price: 179.0<br />Baths: 2.0","Beds: 3<br />Price: 110.0<br />Baths: 1.5","Beds: 3<br />Price: 175.0<br />Baths: 2.0","Beds: 3<br />Price: 100.0<br />Baths: 2.0","Beds: 3<br />Price:  53.0<br />Baths: 1.0","Beds: 3<br />Price:  92.0<br />Baths: 2.0","Beds: 3<br />Price: 127.0<br />Baths: 2.0","Beds: 2<br />Price: 120.5<br />Baths: 2.0","Beds: 3<br />Price:  72.0<br />Baths: 2.0","Beds: 3<br />Price:  95.0<br />Baths: 2.0","Beds: 3<br />Price:  38.5<br />Baths: 1.0","Beds: 4<br />Price: 139.0<br />Baths: 2.0","Beds: 2<br />Price:  75.0<br />Baths: 2.0","Beds: 4<br />Price: 174.0<br />Baths: 3.0","Beds: 4<br />Price: 119.0<br />Baths: 2.0","Beds: 4<br />Price:  89.0<br />Baths: 1.0","Beds: 4<br />Price:  75.1<br />Baths: 2.0","Beds: 3<br />Price:  92.5<br />Baths: 2.0","Beds: 4<br />Price: 141.0<br />Baths: 1.0","Beds: 3<br />Price:  82.0<br />Baths: 3.0","Beds: 4<br />Price: 162.0<br />Baths: 1.5","Beds: 4<br />Price: 195.0<br />Baths: 3.0","Beds: 5<br />Price: 190.0<br />Baths: 3.5","Beds: 4<br />Price: 115.0<br />Baths: 2.0","Beds: 3<br />Price:  87.0<br />Baths: 1.5"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":["rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(237,0,68,1)","rgba(215,0,114,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(255,0,0,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(0,0,255,1)","rgba(141,0,206,1)","rgba(186,0,159,1)","rgba(141,0,206,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(237,0,68,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(237,0,68,1)","rgba(141,0,206,1)","rgba(237,0,68,1)","rgba(255,0,0,1)","rgba(186,0,159,1)","rgba(141,0,206,1)"],"opacity":0.5,"size":5.6692913385826778,"symbol":"circle","line":{"width":1.8897637795275593,"color":["rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(237,0,68,1)","rgba(215,0,114,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(255,0,0,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(0,0,255,1)","rgba(141,0,206,1)","rgba(186,0,159,1)","rgba(141,0,206,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(237,0,68,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(186,0,159,1)","rgba(186,0,159,1)","rgba(0,0,255,1)","rgba(237,0,68,1)","rgba(141,0,206,1)","rgba(237,0,68,1)","rgba(255,0,0,1)","rgba(186,0,159,1)","rgba(141,0,206,1)"]}},"hoveron":"points","showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[2],"y":[50],"name":"99_6ccb91eea3e6eb102a64eebb95be0905","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#0000FF"],[0.0033444816053512126,"#0F00FE"],[0.0066889632107023367,"#1900FD"],[0.01003344481605355,"#2000FD"],[0.013377926421404673,"#2600FC"],[0.016722408026755887,"#2B00FB"],[0.02006688963210701,"#2F00FA"],[0.023411371237458223,"#3300F9"],[0.026755852842809347,"#3700F8"],[0.03010033444816056,"#3A00F8"],[0.033444816053511683,"#3E00F7"],[0.036789297658862893,"#4100F6"],[0.04013377926421402,"#4400F5"],[0.04347826086956523,"#4600F4"],[0.046822742474916357,"#4900F3"],[0.050167224080267567,"#4B00F3"],[0.053511705685618693,"#4E00F2"],[0.056856187290969903,"#5000F1"],[0.06020066889632103,"#5200F0"],[0.06354515050167224,"#5400EF"],[0.066889632107023367,"#5600EF"],[0.070234113712374577,"#5800EE"],[0.073578595317725787,"#5A00ED"],[0.076923076923076913,"#5C00EC"],[0.08026755852842804,"#5E00EB"],[0.08361204013377925,"#6000EB"],[0.08695652173913046,"#6200EA"],[0.090301003344481587,"#6300E9"],[0.093645484949832797,"#6500E8"],[0.096989966555183924,"#6700E7"],[0.10033444816053513,"#6800E6"],[0.10367892976588626,"#6A00E6"],[0.10702341137123747,"#6B00E5"],[0.1103678929765886,"#6D00E4"],[0.11371237458193981,"#6E00E3"],[0.11705685618729093,"#7000E2"],[0.12040133779264214,"#7100E2"],[0.12374581939799327,"#7200E1"],[0.12709030100334448,"#7400E0"],[0.1304347826086957,"#7500DF"],[0.13377926421404682,"#7600DE"],[0.13712374581939796,"#7800DE"],[0.14046822742474915,"#7900DD"],[0.14381270903010038,"#7A00DC"],[0.14715719063545149,"#7B00DB"],[0.15050167224080263,"#7D00DA"],[0.15384615384615383,"#7E00DA"],[0.15719063545150505,"#7F00D9"],[0.16053511705685616,"#8000D8"],[0.16387959866220739,"#8100D7"],[0.1672240802675585,"#8200D6"],[0.17056856187290972,"#8400D5"],[0.17391304347826084,"#8500D5"],[0.17725752508361206,"#8600D4"],[0.18060200668896317,"#8700D3"],[0.1839464882943144,"#8800D2"],[0.18729096989966551,"#8900D1"],[0.19063545150501673,"#8A00D1"],[0.19397993311036785,"#8B00D0"],[0.19732441471571907,"#8C00CF"],[0.20066889632107027,"#8D00CE"],[0.20401337792642141,"#8E00CD"],[0.20735785953177252,"#8F00CD"],[0.21070234113712374,"#9000CC"],[0.21404682274247494,"#9100CB"],[0.21739130434782608,"#9200CA"],[0.22073578595317719,"#9300CA"],[0.22408026755852842,"#9400C9"],[0.22742474916387961,"#9400C8"],[0.23076923076923075,"#9500C7"],[0.23411371237458187,"#9600C6"],[0.23745819397993309,"#9700C6"],[0.24080267558528429,"#9800C5"],[0.24414715719063543,"#9900C4"],[0.24749163879598654,"#9A00C3"],[0.25083612040133774,"#9B00C2"],[0.25418060200668896,"#9B00C2"],[0.25752508361204018,"#9C00C1"],[0.2608695652173913,"#9D00C0"],[0.26421404682274241,"#9E00BF"],[0.26755852842809363,"#9F00BE"],[0.27090301003344486,"#9F00BE"],[0.27424749163879597,"#A000BD"],[0.27759197324414708,"#A100BC"],[0.28093645484949831,"#A200BB"],[0.28428093645484953,"#A300BA"],[0.28762541806020064,"#A300BA"],[0.29096989966555176,"#A400B9"],[0.29431438127090298,"#A500B8"],[0.2976588628762542,"#A600B7"],[0.30100334448160532,"#A600B7"],[0.30434782608695643,"#A700B6"],[0.30769230769230765,"#A800B5"],[0.31103678929765888,"#A800B4"],[0.31438127090300999,"#A900B3"],[0.3177257525083611,"#AA00B3"],[0.32107023411371233,"#AB00B2"],[0.32441471571906355,"#AB00B1"],[0.32775919732441477,"#AC00B0"],[0.33110367892976589,"#AD00AF"],[0.334448160535117,"#AD00AF"],[0.33779264214046822,"#AE00AE"],[0.34113712374581945,"#AF00AD"],[0.34448160535117056,"#AF00AC"],[0.34782608695652167,"#B000AC"],[0.3511705685618729,"#B100AB"],[0.35451505016722412,"#B100AA"],[0.35785953177257523,"#B200A9"],[0.36120401337792635,"#B300A8"],[0.36454849498327757,"#B300A8"],[0.3678929765886288,"#B400A7"],[0.37123745819397991,"#B400A6"],[0.37458193979933102,"#B500A5"],[0.37792642140468224,"#B600A5"],[0.38127090301003347,"#B600A4"],[0.38461538461538458,"#B700A3"],[0.38795986622073569,"#B700A2"],[0.39130434782608692,"#B800A1"],[0.39464882943143814,"#B900A1"],[0.39799331103678937,"#B900A0"],[0.40133779264214053,"#BA009F"],[0.40468227424749159,"#BA009E"],[0.40802675585284282,"#BB009E"],[0.41137123745819404,"#BC009D"],[0.41471571906354504,"#BC009C"],[0.41806020066889626,"#BD009B"],[0.42140468227424749,"#BD009B"],[0.42474916387959849,"#BE009A"],[0.42809364548494988,"#BE0099"],[0.43143812709030094,"#BF0098"],[0.43478260869565216,"#BF0097"],[0.43812709030100339,"#C00097"],[0.44147157190635439,"#C10096"],[0.44481605351170578,"#C10095"],[0.44816053511705684,"#C20094"],[0.45150501672240806,"#C20094"],[0.45484949832775923,"#C30093"],[0.45819397993311028,"#C30092"],[0.46153846153846151,"#C40091"],[0.46488294314381273,"#C40091"],[0.46822742474916373,"#C50090"],[0.47157190635451512,"#C5008F"],[0.47491638795986618,"#C6008E"],[0.47826086956521741,"#C6008D"],[0.48160535117056857,"#C7008D"],[0.48494983277591963,"#C7008C"],[0.48829431438127086,"#C8008B"],[0.49163879598662208,"#C8008A"],[0.49498327759197308,"#C9008A"],[0.49832775919732447,"#C90089"],[0.50167224080267547,"#CA0088"],[0.50501672240802675,"#CA0087"],[0.50836120401337792,"#CB0087"],[0.51170568561872898,"#CB0086"],[0.51505016722408037,"#CC0085"],[0.51839464882943143,"#CC0084"],[0.52173913043478259,"#CD0084"],[0.52508361204013387,"#CD0083"],[0.52842809364548482,"#CE0082"],[0.5317725752508361,"#CE0081"],[0.53511705685618727,"#CE0080"],[0.53846153846153832,"#CF0080"],[0.54180602006688972,"#CF007F"],[0.54515050167224077,"#D0007E"],[0.54849498327759194,"#D0007D"],[0.55183946488294322,"#D1007D"],[0.55518394648829417,"#D1007C"],[0.55852842809364545,"#D2007B"],[0.56187290969899661,"#D2007A"],[0.56521739130434767,"#D3007A"],[0.56856187290969906,"#D30079"],[0.57190635451505012,"#D30078"],[0.57525083612040129,"#D40077"],[0.57859531772575257,"#D40077"],[0.58193979933110351,"#D50076"],[0.5852842809364549,"#D50075"],[0.58862876254180596,"#D60074"],[0.59197324414715724,"#D60074"],[0.59531772575250841,"#D60073"],[0.59866220735785947,"#D70072"],[0.60200668896321063,"#D70071"],[0.60535117056856191,"#D80071"],[0.60869565217391286,"#D80070"],[0.61204013377926425,"#D8006F"],[0.61538461538461531,"#D9006E"],[0.61872909698996659,"#D9006E"],[0.62207357859531776,"#DA006D"],[0.62541806020066881,"#DA006C"],[0.62876254180601998,"#DA006B"],[0.63210702341137126,"#DB006A"],[0.63545150501672221,"#DB006A"],[0.6387959866220736,"#DC0069"],[0.64214046822742465,"#DC0068"],[0.64548494983277593,"#DC0067"],[0.6488294314381271,"#DD0067"],[0.65217391304347816,"#DD0066"],[0.65551839464882955,"#DE0065"],[0.65886287625418061,"#DE0064"],[0.66220735785953178,"#DE0064"],[0.66555183946488294,"#DF0063"],[0.668896321070234,"#DF0062"],[0.67224080267558528,"#E00061"],[0.67558528428093645,"#E00061"],[0.67892976588628751,"#E00060"],[0.6822742474916389,"#E1005F"],[0.68561872909698995,"#E1005E"],[0.68896321070234112,"#E1005E"],[0.69230769230769229,"#E2005D"],[0.69565217391304335,"#E2005C"],[0.69899665551839463,"#E3005B"],[0.7023411371237458,"#E3005B"],[0.70568561872909685,"#E3005A"],[0.70903010033444824,"#E40059"],[0.7123745819397993,"#E40058"],[0.71571906354515047,"#E40057"],[0.71906354515050164,"#E50057"],[0.72240802675585269,"#E50056"],[0.72575250836120409,"#E50055"],[0.72909698996655514,"#E60054"],[0.73244147157190631,"#E60054"],[0.73578595317725759,"#E60053"],[0.73913043478260865,"#E70052"],[0.74247491638795982,"#E70051"],[0.74581939799331098,"#E80050"],[0.74916387959866204,"#E80050"],[0.75250836120401343,"#E8004F"],[0.75585284280936449,"#E9004E"],[0.75919732441471566,"#E9004D"],[0.76254180602006694,"#E9004D"],[0.76588628762541799,"#EA004C"],[0.76923076923076916,"#EA004B"],[0.77257525083612033,"#EA004A"],[0.77591973244147139,"#EB0049"],[0.77926421404682278,"#EB0049"],[0.78260869565217384,"#EB0048"],[0.785953177257525,"#EC0047"],[0.78929765886287628,"#EC0046"],[0.79264214046822734,"#EC0046"],[0.79598662207357873,"#ED0045"],[0.79933110367892968,"#ED0044"],[0.80267558528428096,"#ED0043"],[0.80602006688963213,"#EE0042"],[0.80936454849498318,"#EE0042"],[0.81270903010033435,"#EE0041"],[0.81605351170568563,"#EF0040"],[0.8193979933110368,"#EF003F"],[0.82274247491638786,"#EF003E"],[0.82608695652173902,"#F0003D"],[0.8294314381270903,"#F0003D"],[0.83277591973244147,"#F0003C"],[0.83612040133779253,"#F0003B"],[0.8394648829431437,"#F1003A"],[0.84280936454849498,"#F10039"],[0.84615384615384615,"#F10038"],[0.8494983277591972,"#F20038"],[0.85284280936454837,"#F20037"],[0.85618729096989965,"#F20036"],[0.85953177257525082,"#F30035"],[0.8628762541806021,"#F30034"],[0.86622073578595304,"#F30033"],[0.86956521739130432,"#F40032"],[0.87290969899665549,"#F40032"],[0.87625418060200677,"#F40031"],[0.87959866220735772,"#F50030"],[0.882943143812709,"#F5002F"],[0.88628762541806017,"#F5002E"],[0.88963210702341144,"#F5002D"],[0.89297658862876239,"#F6002C"],[0.89632107023411367,"#F6002B"],[0.89966555183946484,"#F6002A"],[0.90301003344481612,"#F70029"],[0.90635451505016706,"#F70028"],[0.90969899665551834,"#F70027"],[0.91304347826086951,"#F80026"],[0.91638795986622079,"#F80025"],[0.91973244147157174,"#F80024"],[0.92307692307692302,"#F80023"],[0.92642140468227419,"#F90022"],[0.92976588628762546,"#F90021"],[0.93311036789297663,"#F90020"],[0.93645484949832769,"#FA001F"],[0.93979933110367886,"#FA001E"],[0.94314381270903014,"#FA001D"],[0.94648829431438131,"#FA001B"],[0.94983277591973236,"#FB001A"],[0.95317725752508353,"#FB0019"],[0.95652173913043481,"#FB0018"],[0.95986622073578598,"#FC0016"],[0.96321070234113704,"#FC0015"],[0.96655518394648821,"#FC0013"],[0.96989966555183948,"#FC0012"],[0.97324414715719065,"#FD0010"],[0.97658862876254171,"#FD000F"],[0.97993311036789288,"#FD000D"],[0.98327759197324416,"#FE000B"],[0.98662207357859533,"#FE0008"],[0.98996655518394638,"#FE0006"],[0.99331103678929755,"#FE0004"],[0.99665551839464883,"#FF0002"],[1,"#FF0000"]],"colorbar":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.8897637795275593,"thickness":23.039999999999996,"title":"Baths","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724},"tickmode":"array","ticktext":["1.0","1.5","2.0","2.5","3.0","3.5"],"tickvals":[0,0.20000000000000001,0.40000000000000002,0.59999999999999998,0.80000000000000004,1],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.68949771689498},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":26.228310502283108,"r":7.3059360730593621,"b":40.182648401826498,"l":43.105022831050235},"plot_bgcolor":"rgba(255,255,255,1)","paper_bgcolor":"rgba(255,255,255,1)","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[1.8,6.2000000000000002],"tickmode":"array","ticktext":["2","3","4","5","6"],"tickvals":[2,3,4,5,6],"categoryorder":"array","categoryarray":["2","3","4","5","6"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176002,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"Beds","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[30.550000000000001,205.44999999999999],"tickmode":"array","ticktext":["50","100","150","200"],"tickvals":[50,100,150,200],"categoryorder":"array","categoryarray":["50","100","150","200"],"nticks":null,"ticks":"outside","tickcolor":"rgba(51,51,51,1)","ticklen":3.6529680365296811,"tickwidth":0.66417600664176002,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.68949771689498},"tickangle":-0,"showline":true,"linecolor":"rgba(0,0,0,1)","linewidth":0.66417600664176002,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"x","title":{"text":"Price","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":"rgba(255,255,255,1)","bordercolor":"transparent","borderwidth":1.8897637795275593,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.68949771689498},"title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.611872146118724}}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"source":"A","attrs":{"12fb5576960ab":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"12fb5576960ab","visdat":{"12fb5576960ab":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

Many more interactive options in this tutorial: <https://plotly.com/r/line-and-scatter/>



### Histograms

Especially just looking at a single response variable, it's useful to look immediately at the distribution itself. Histograms are great for this, although you must be careful that the bin size doesn't impact your perception of results. Adding in a boxplot is often useful

#### Basics 

Here is the absolute basic histogram


```r
hist(HousesNY$Price)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-9-1.png" width="672" />

Or changing the bin size


```r
hist(HousesNY$Price,br=40)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-10-1.png" width="672" />

In GGPlot 2, it's also easy. Remember to install the ggplot2 package.


```r
ggplot(data=HousesNY, aes(x=Price)) + 
  geom_histogram(bins=20) 
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-11-1.png" width="672" />

#### Adding a boxplot and histogram

Often, a boxplot AND a histogram is useful as it allows you to see a sense of the data shape and its underlying symmetry. For example, in base R


```r
# Layout to split the screen
graphics::layout(matrix(c(1,2),2,1, byrow=TRUE),  
       height = c(2,7))
 
# Draw the boxplot and the histogram 
par(mar=c(0, 3.1, .5, 2.1))

data_to_plot <- HousesNY$Price

rangeplot <- pretty(data_to_plot,10)

boxplot(data_to_plot,col = "light blue",
        border = "dark blue",xaxt="n",frame=FALSE,xlim=c(0.75,1.25),
        horizontal = TRUE,notch = TRUE,ylim=c(min(rangeplot),max(rangeplot)))

par(mar=c(3, 3.1, .5, 2.1))
hist(data_to_plot , breaks=20 , 
     col=grey(0.3) , border=F , 
     tcl=-.25,mgp=c(1.75,.5,0),
     main="" , xlab="Price of houses in Canton NY", 
     xlim=c(min(rangeplot),max(rangeplot)))
box();grid();
hist(data_to_plot , breaks=20 , add=TRUE,
     col=grey(0.3) , border=F , axis=FALSE,
     xlim=c(min(rangeplot),max(rangeplot)))
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-12-1.png" width="672" />

And the same with ggplot2:


```r
library(ggExtra)

p <- ggplot(data=HousesNY, aes(x=Price)) + 
  geom_point(aes(y = 0.01), alpha = 0) +
  geom_histogram(bins=20) +
  geom_density(na.rm=T)

ggMarginal(p, type="boxplot", margins = "x")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-13-1.png" width="672" />

I also love the ggstatplot version


```r
library(ggstatsplot)
## plot
gghistostats(
  data       = HousesNY, ## dataframe from which variable is to be taken
  x          = Price, ## numeric variable whose distribution is of interest
  title      = "Price of sampled houses in Canton NY", ## title for the plot
  caption    = "Source: Zillow",
  type = "parametric",
  xlab = NULL,subtitle=FALSE,
  ggthemes::theme_tufte(),
  binwidth   = 8) ## binwidth value (experiment)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-14-1.png" width="672" />

Or their version that includes a lot of associated statistics. You can turn many of these on and off


```r
library(ggstatsplot)

## plot
gghistostats(
  data       = HousesNY, ## dataframe from which variable is to be taken
  x          = Price, ## numeric variable whose distribution is of interest
  title      = "Price of sampled houses in Canton NY", ## title for the plot
  caption    = "Source: Zillow",
  type = "parametric",
  xlab = NULL,
  ggthemes::theme_tufte(),
  binwidth   = 8) ## binwidth value (experiment)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-15-1.png" width="672" />

#### Adding a density function

Sometimes seeing a smoothed line helps draw the eye to distributions


```r
hist(HousesNY$Price, prob = TRUE,
     main = "Canton Prices with density curve")
lines(density(HousesNY$Price), col = 4, lwd = 2)
box()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-16-1.png" width="672" />

#### Adding a distribution

Let's say you want to make plots similar to the ones in the lectures where there is your chosen distribution on top.

If you know the distribution, you can simply add it on top as a line


```r
mysample <- HousesNY$Price

plotmin <- mean(mysample) - sd(mysample)*3
plotmax <-  mean(mysample) + sd(mysample)*3

# Points for the normal equation line
NormCurve_x <- seq(plotmin,plotmax, length = 40)

# Normal curve calculation for each point
NormCurve_y <- dnorm(NormCurve_x, mean = mean(mysample), sd = sd(mysample))

# make sure this is density not raw frequency
hist(mysample , breaks=20 , freq=FALSE,
     col=grey(0.5) , border=F , 
     xlim=c(plotmin,plotmax),
     tcl=-.25,mgp=c(1.75,.5,0),
     main="" , xlab="Price of houses in Canton NY")
# add the normal curve (THIS NEEDS TO BE IN THE SAME CODE CHUNK)
lines(NormCurve_x, NormCurve_y, col = 2, lwd = 2)
box()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-17-1.png" width="672" />

We could plot any old curve this way, it doesn't have to be "fit" to our data. For example here is a random gamma function


```r
mysample <- HousesNY$Price

# Points for the normal equation line
GammaCurve_x <- seq(plotmin,plotmax, length = 60)
GammaCurve_y <- dgamma(GammaCurve_x,shape = 2)

# make sure this is density not raw frequency
hist(mysample , breaks=20 , freq=FALSE,
     col=grey(0.5) , border=F , 
     xlim=c(plotmin,plotmax),
     tcl=-.25,mgp=c(1.75,.5,0),
     main="" , xlab="Price of houses in Canton NY")
# add the normal curve (THIS NEEDS TO BE IN THE SAME CODE CHUNK)
lines(GammaCurve_x, GammaCurve_y, col = 2, lwd = 2)
box()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-18-1.png" width="672" />

#### Comparing groups

Or you can easily compare two datasets, tutorial for this plot here: <https://www.r-graph-gallery.com/histogram_several_group.html>

<br> <br>

### Boxplots {#T6_boxplots}

Boxplots have been around over 40 years! See their history and evolution here: <http://vita.had.co.nz/papers/boxplots.pdf>

In terms of your reports, you need to think of 3 things: - Why you are making the plot (quick look vs publication worthy final graphic) - What aspects of the data do you want to highlight (lots of data, comparing groups, weird distributions..) - What are your final requirements and personal style (colorblind friendly, you're drawn to a certain type of plot..)

So for boxplots.. they are especially good at allowing you to compare different groups of things or to look for multiple groups in a single response variable. Here is a beautiful example made by Marcus Beckman on dissertation lengths.

[https://beckmw.wordpress.com/2014/07/15/average-dissertation-and-thesis-length-take-two/ and code here: https://github.com/fawda123/diss_proc](https://beckmw.wordpress.com/2014/07/15/average-dissertation-and-thesis-length-take-two/%20and%20code%20here:%20https://github.com/fawda123/diss_proc) )

If there are only one or two variables, I often jump to the violin or histogram plots as they show more detail.

So.. how to make these yourselves. You have a range of options!

#### Basics (single boxplot)

Here is the most basic boxplot you can make. I often start with this for my own use when exploring the data, then later decide which plots to "make pretty".


```r
boxplot(HousesNY$Price)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-19-1.png" width="672" />

We can make better boxplots in base R (e.g. using no special packages/libraries). See this tutorial for all the details: <https://www.datamentor.io/r-programming/box-plot/> which goes through exactly what each line means.


```r
# one big command on separate lines
boxplot(HousesNY$Price,
        main = "House prices of Canton NY sample",
        xlab = "Price (Thousand USD)",
        col = "light blue",
        border = "dark blue",
        horizontal = TRUE,
        notch = TRUE)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-20-1.png" width="672" />

There are specific plotting packages, the most famous being ggplot2 (there are data camp courses on it). The absolute basics. Here x is blank because we just want to look at the price column alone.


```r
library(ggplot2)

ggplot(HousesNY, aes(x ="", y = Price)) +    ## this loads the data
   geom_boxplot()                            ## and we choose a boxplot
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-21-1.png" width="672" />

Note for now, think of the %\>% symbol and + symbol also as "one command on multiple lines..". They allow you to build up layers of the plot. Data camp has more on this.

But with these we can easily do more sophisticated things. For example, here's how to see the underlying data, which allows us to see something of the background distribution

<https://r-charts.com/distribution/box-plot-jitter-ggplot2/>


```r
# Basic box plot
ggplot(HousesNY, aes(x = "", y = Price)) + 
  geom_boxplot() +
  geom_jitter()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-22-1.png" width="672" />

#### Comparing groups

The basic code to see a boxplot split by group, in this case the price per number of beds:


```r
boxplot(HousesNY$Price ~ HousesNY$Beds)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-23-1.png" width="672" />

The advantage of this is that you can be sure that you really did plot your columns of choice (e.g. you didn't mistakenly label anything). Note, if you use a comma, rather than the "\~" symbol, you will make one for each column - which is normally not useful!


```r
boxplot(HousesNY$Price,  HousesNY$Beds)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-24-1.png" width="672" />

<br>

In GGplot comparing different groups:


```r
# Libraries
library(tidyverse)
library(hrbrthemes)
library(viridis)

# tell R that the beds column is categorical
HousesNY$Beds <- factor(HousesNY$Beds,
                     levels=c(min(HousesNY$Beds):max(HousesNY$Beds)))

# Plot
  ggplot(HousesNY, aes(x=Beds, y=Price)) +
    geom_boxplot() 
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-25-1.png" width="672" />

Or getting more complex


```r
# Libraries
library(tidyverse)
library(hrbrthemes)
library(viridis)

# tell R that the beds column is categorical
# I already did this in the table section
#HousesNY$Beds <- as.factor(HousesNY$Beds)

# Plot
HousesNY %>%
  ggplot( aes(x=Beds, y=Price, fill=Beds) )+
    geom_boxplot() +
    scale_fill_viridis(discrete = TRUE, alpha=0.6) +
    geom_jitter(color="black", size=0.5, alpha=0.8) +
    ggtitle("") +
    xlab("Beds")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-26-1.png" width="672" />

or dotplots..


```r
ggplot(HousesNY,  aes(x=Beds, y=Price, fill=Beds)) +
  geom_boxplot() +
  geom_dotplot(binaxis = "y", stackdir = "center", dotsize = 0.5,binwidth=7)
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-27-1.png" width="672" />

There are MANY more options, plus code here: <https://www.r-graph-gallery.com/boxplot.html>

and a delightful tutorial here: <https://www.r-bloggers.com/2021/11/how-to-make-stunning-boxplots-in-r-a-complete-guide-with-ggplot2/>

#### Sophisticated

Finally, we *can* get super fancy in base R - it's often a good way to learn how to code. I like this example because it shows many different aspects/useful commands in R programming. <http://www.opiniomics.org/beautiful-boxplots-in-base-r/>


```r
library(RColorBrewer)

# create colours and colour matrix (for points)
m     <- as.matrix(HousesNY$Price)

col_main   <- colorRampPalette(brewer.pal(12, "Set3"), alpha=TRUE)(ncol(m))
col_transp <- colorspace::adjust_transparency(col_main, alpha = .3)

colsm   <-matrix(rep(col_main, each=nrow(m)), ncol=ncol(m))
colsm_tr <-matrix(rep(col_transp, each=nrow(m)), ncol=ncol(m))


# create some random data for jitter
r <-  (matrix(runif(nrow(m)*ncol(m)), nrow=nrow(m), ncol=ncol(m)) / 2) - 0.25

# get the greys (stolen from https://github.com/zonination/perceptions/blob/master/percept.R)
palette <- brewer.pal("Greys", n=9)
color.background = palette[2]
color.grid.major = palette[5]

# set graphical area
par(bty="n", bg=palette[2], mar=c(5,8,3,1))

# plot initial boxplot
boxplot(m~col(m), horizontal=TRUE, outline=FALSE, lty=1, 
        staplewex=0, boxwex=0.8, boxlwd=1, medlwd=1, 
        col=colsm_tr, xaxt="n", yaxt="n",xlab="",ylab="")

# plot gridlines
for (i in pretty(m,10)) {
	lines(c(i,i), c(0,20), col=palette[4])
}

# plot points
points(m, col(m)+r, col=colsm, pch=16)

# overlay boxplot
boxplot(m~col(m), horizontal=TRUE, outline=FALSE, lty=1, 
        staplewex=0, boxwex=0.8, boxlwd=1, medlwd=1, col=colsm_tr, 
        add=TRUE, xaxt="n", yaxt="n")

# add axes and title
axis(side=1, at=pretty(m,10), col.axis=palette[7], 
     cex.axis=0.8, lty=0, tick=NA, line=-1)
axis(side=1, at=50, labels="Price (Thousand USD)", 
     lty=0, tick=NA, col.axis=palette[7])
axis(side=2, at=1, col.axis=palette[7], cex.axis=0.8, 
     lty=0, tick=NA, labels="Sample 1", las=2)
axis(side=2, at=17/2, labels="Phrase", col.axis=palette[7], 
     lty=0, tick=NA, las=3, line=6)
title("House Prices in Canton NY")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-28-1.png" width="672" />

Or if you wish to do the rainbow many group boxplot at the beginning, the code is here : <https://github.com/fawda123/diss_proc/blob/master/diss_plot.R>

<br> <br>

### Violin plots

Violin plots combine the simplicity of a boxplot with a sense of the underlying distribution. This is useful when you want a sense of both the symmetry of the data and the underlying distribution. Highly recommended! For a single variable, consider a box-plot-with-histogram (see below).

There are MANY on R graph gallery with code you can copy/edit: <https://www.r-graph-gallery.com/violin.html>

For example, for our data:


```r
# fill=name allow to automatically dedicate a color for each group
ggplot(HousesNY, aes(x=Beds, y=Price, fill=Beds)) + 
   geom_violin()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-29-1.png" width="672" />

There's also a *beautiful* package called `ggstatsplot` which allows a lot of detail (<https://indrajeetpatil.github.io/ggstatsplot/>)

For example, I love the plot below because it shows how much data in each group.


```r
# you might need to first install this.
library(ggstatsplot)

# i'm changing the middle mean point to be dark blue

ggbetweenstats(data = HousesNY,x = Beds,y = Price, 
               centrality.point.args=list(color = "darkblue"))
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-30-1.png" width="672" />

Or we can customise it even more using this tutorial to get results like this (<https://www.r-graph-gallery.com/web-violinplot-with-ggstatsplot.html>)

<br> <br>

### Ridgeline plots

These are another way of looking at histograms for different groups. They work especially when your grouping data is ORDINAL (has some inherent order). So bedrooms would be a good example

Two great pages here:

-   <https://www.data-to-viz.com/graph/ridgeline.html>

-   <https://r-charts.com/distribution/ggridges/>

We can use histograms or smoothed density lines <https://www.data-to-viz.com/graph/ridgeline.html>


```r
library(ggridges)
library(ggplot2)

HousesNY %>%
  ggplot( aes(y=Beds, x=Price,  fill=Beds)) +
    geom_density_ridges(alpha=0.6, stat="binline") +
    scale_fill_viridis(discrete=TRUE) +
    scale_color_viridis(discrete=TRUE) +
    theme_ipsum() +
    theme(
      legend.position="none",
      panel.spacing = unit(0.1, "lines"),
      strip.text.x = element_text(size = 8)
    ) +
    xlab("") +
    ylab("Number of Bedrooms")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-31-1.png" width="672" />

All of these are from <https://r-charts.com/distribution/ggridges/>


```r
library(ggridges)
library(ggplot2)

ggplot(HousesNY, aes(x = Price, y = Beds, fill = stat(x))) +
  geom_density_ridges_gradient() +
  scale_fill_viridis_c(name = "Depth", option = "C") +
  coord_cartesian(clip = "off") + # To avoid cut off
  theme_minimal()
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-32-1.png" width="672" />

We can also make the colours more meaningful, for example adding quantiles to show the median and interquartile range


```r
ggplot(HousesNY, aes(x = Price, y = Beds, fill = stat(quantile))) +
  stat_density_ridges(quantile_lines = FALSE,
                      calc_ecdf = TRUE,
                      geom = "density_ridges_gradient") +
  scale_fill_brewer(name = "")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-33-1.png" width="672" />

or highlighting tails


```r
ggplot(HousesNY, aes(x = Price, y = Beds, fill = stat(quantile))) +
  stat_density_ridges(quantile_lines = TRUE,
                      calc_ecdf = TRUE,
                      geom = "density_ridges_gradient",
                      quantiles = c(0.05, 0.95)) +
  scale_fill_manual(name = "Proportion", 
                    values = c("#E2FFF2", "white", "#B0E0E6"),
                    labels = c("(0, 5%]", "(5%, 95%]", "(95%, 1]"))
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-34-1.png" width="672" />

### Beeswarm plots

These are cool. As described here:

[https://www.rhoworld.com/i-swarm-you-swarm-we-all-swarm-for-beeswarm-plots-0/#:\~:text=What%20is%20a%20beeswarm%20plot%3F&text=A%20beeswarm%20plot%20improves%20upon,bees%20buzzing%20about%20their%20hive.](https://www.rhoworld.com/i-swarm-you-swarm-we-all-swarm-for-beeswarm-plots-0/#:~:text=What%20is%20a%20beeswarm%20plot%3F&text=A%20beeswarm%20plot%20improves%20upon,bees%20buzzing%20about%20their%20hive)

"But what is a beeswarm plot? ... A beeswarm plot improves upon the random jittering approach to move data points the minimum distance away from one another to avoid overlays. The result is a plot where you can see each distinct data point, like so: It looks a bit like a friendly swarm of bees buzzing about their hive."

It's often used for professional visualisation, see here for many examples: <https://flowingdata.com/charttype/beeswarm>

Especially for the first, you can see the distribution clearly, also with the amount of data. With the second, you can see the mitigating impact of a second variable.

To make easy ones you can install a new packages "beeswarm"


```r
library("beeswarm")

beeswarm(HousesNY$Price,
         vertical = FALSE, method = "hex")
```

<img src="in_04-Tutorial6_Plots_files/figure-html/unnamed-chunk-35-1.png" width="672" />

This is a little boring for my 58 data points! (although perhaps it does show that 58 points is barely a big enough sample to know an underlying model..)

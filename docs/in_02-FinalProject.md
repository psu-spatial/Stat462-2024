

# Final Project {.unnumbered}

## Aim {.unnumbered}

Welcome to your final project. This is worth 160 points (similar to an exam), compared to your labs which were worth 100 points.\
Remember you can drop either this or your lowest exam grade

By the end of this lab, you will be able to:

1.  Showcase your knowledge of simple linear regression
2.  Carry this forward into a mulitple regression analysis
3.  Use your models to predict a real-life messy dataset.

You need to submit your report by Wed May 1, 23:59pm. If you are going to be late, you have 3 options:

1.  Especially if you are graduating, you can use this as your drop. Submit what you have and focus on the exam
2.  If you are NOT graduating and struggling to get it done, I am happy to formally defer your grade to give you a little more support.

<br>

### Need help? {.unnumbered}

**Code won't knit? Struggling? Have a question? See the help page here: [Help!](#Help)**

<br>

## 1. Set up (DON'T SKIP) {.unnumbered}

<br>

### **[Step 1.1] Create a new project for your project** {.unnumbered}

-   I am assuming you now know how to do this. See previous labs and the tutorial

<br><br>

### **[Step 1.2] Go to Canvas and get your personalised data.** {.unnumbered}

-   You each get your own individual dataset, sampled out of a large population. You can download this from Canvas.

<br><br>

### **[Step 1.3] Create a lab report template** {.unnumbered}

-   I expect your report to look professional, with a floating table of contents, a report title and the date in your YAML code (AKA exactly what I have asked in the other labs). You now have many templates:

    -   You could copy over a previous one that you like and just delete your code, use one I provided and/or create your own using tutorial 3 (<https://psu-spatial.github.io/Stat462-2024/T3_Markdown.html#T3_YAML>). <br>

    -   Remember that in the template for lab 6, I have summarized all the linear regression code in a bundle that you can copy/paste to save time.<br>

    -   I suggest copy/pasting your initial library code chunk from Lab 6, then you have those options set and your libraries already loaded.

    -   Press knit and make sure it all works. OR TALK TO DR G.

<br><br>

------------------------------------------------------------------------

## 2. The AirBnB challenge (READ THIS!) {.unnumbered}

You are an analyst for the holiday rental company, AirBnB. You have been paid to answer some questions that the company has about their rentals in San Francisco. They are especially interested in understanding if you can predict rental prices given recent fears about a crash (see below)

AirBnB have provided you a sample dataset of 150 AirBnb rentals from March-05-2023 in San Francisco. Your professor has also merged this with a load of demographics data from the US Census. Overall you have this data:

Your unit of analysis is an individual rental on a specific day and your RESPONSE variable is price.

Here is your full list of variables and their units/sources:

### **[Step 2.1] Write up a brief introduction (\~ 100 words)** {.unnumbered}

In your report, write up a brief introduction about AirBnb rentals in San Francisco and what you think might be driving rental prices. Consider including a picture/photo to make it look even more professional (imagine a consultancy style report you can share in your job interview). These links might help:

-   <https://news.airbnb.com/about-us/>

-   <https://sfstandard.com/2023/07/05/san-francisco-airbnb-bookings-plunge-as-city-battles-bad-press/>

-   <https://www.newsweek.com/airbnb-revenue-collapse-housing-market-crash-fears-1809543>

Given what you read above (e.g. using your own common sense), write a prediction of which variable(s) you THINK might most impact house prices.

**Remember to use headings and subheadings to make it easy to read**

<br><br>

### **[Step 2.2] Read in your sample data** {.unnumbered}

You should have downloaded TWO files from the canvas link. Both should have your email ID on them,

-   The first file contains 150 individual room rentals in San Francisco from May 2023

-   The other file contains 150 ENTIRE HOUSE rentals in San Francisco from May 2023

Use the `read_excel()` command to load the data into R. I suggest assigning the room data to a variable called `room` and the other to a variable called `house`. If you are stuck see (<https://psu-spatial.github.io/Stat462-2024/T4_ReadingData.html#T4_readxl>)

<br><br>

### **[Step 2.3] Now make a spatial version** {.unnumbered}

Just like with the Taiwan dataset, you have a spatial component and so you are able to make maps in order to better understand your dataset. To do this:

1.  Make sure that the `sf` , `corrplot` and `tmap` libraries are both installed AND loaded in your library code chink at the top.

2.  Adjust this code to match your variable names and run. R will now understand that room.sf is a spatial dataset - in step 2.4 you can make some maps.


```r
# adjust to whatever you called your datasets. the 4326 means lat/long
room.sf <- st_as_sf(room,coords=c("Longitude","Latitude"),crs=4326)
house.sf <- st_as_sf(house,coords=c("Longitude","Latitude"),crs=4326)
```

<br><br>

### **[Step 2.4] Summarise** THE ROOM DATASET {.unnumbered}

Use summary code to describe the dataset. I suggest first copying over the table in these in these instructions into the text so you have a list of variables.

Then you can use your summary code and common sense to report things like how much data you have, what your response variable looks like, if there are any notable outliers, any interesting relationships and any correlations. You can use old code from your old labs! Also included here in the tutorials

-   Summary code:<https://psu-spatial.github.io/Stat462-2024/T9_wrangling.html#summary-statistics>

-   Plots: <https://psu-spatial.github.io/Stat462-2024/T6_plots.html>

-   Correlation matrices (I suggest the corrplot one): <https://psu-spatial.github.io/Stat462-2024/correlation.html>

-   Maps:

    -   The easiest map you can make is a "quick thematic map", `qtm` from the tmap package

    -   For example, this should run on your spatial data.


```r
# on the cloud, try tmap_mode("plot"), or don't make maps
tmap_mode("view")
qtm(room.sf,dots.col="price",title="AirBnB Price",dots.size=.5,dots.palette="Blues")
```

For more fancy maps (that aren't much harder), see here = BUT KNOW YOU'RE SWITCHING TUTORIAL TO MY OTHER COURSE! You can also see how to extract things like elevation data if you want even more variables.

-   <https://psu-spatial.github.io/Geog364-2021/364Data_TutorialWranglePoint.html>

**As well as your code/analysis/plots, I expect you to write around 100 words, explaining what you see. Remember headings/subheadings to make it easy to follow! Including "**`<br>`" will also give you a line of white space - it's how I separate my sections.

<br><br>

------------------------------------------------------------------------

## 3. Simple Linear Regression {.unnumbered}

<br>

### **[Step 3.1]** Get the code running {.unnumbered}

Choose [**TWO**]{.underline} variables that you think might predict airbnb prices FOR THE ROOM DATASET. Briefly explain why you chose those two variables in your report, using your summary analysis above to justify your choice.

Conduct TWO SEPARATE simple linear regression analyses, one for each variable - with the response as price.

-   For each, include a professional scatterplot

-   Assess LINE/outliers

-   And summarise model in the text.

### **[Step 3.2]** Compare the models {.unnumbered}

See tutorial 15 onwards. Compare your two models in terms of:

1.  The percentage variability explained

2.  AIC

3.  The effect (slope) size

4.  Whether the slope is significant

5.  Meeting the LINE assumptions

At the end, explain which model you would choose so far.

<br><br><br>

------------------------------------------------------------------------

## 4. MULTIPLE REGRESSION {.unnumbered}

WE WILL TALK ABOUT THIS IN CLASS TODAY

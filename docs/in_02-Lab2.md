

# Lab 2 {#Lab_2 .unnumbered}

## Aim

Welcome to lab 2. This is worth 10% (100 points) and you can drop your lowest lab out of six. The aim of the lab is to continue getting used to some basic exploratory data analysis, including

-   Getting help

-   Reading in data

-   Dealing with missing data

-   Making nice plots & summary statistics

This is a ONE WEEK LAB. You only have one lab session (today) working on this during class, then 10 days to finish up and write up. The maximum time it should take is about 4-5 hrs of your time. [**If you are stuck, ask for help**]{.underline}.

<br>

------------------------------------------------------------------------

## Instructions {.unnumbered}

### Set up (DON'T SKIP) {.unnumbered}

**[1] Create a project for Lab 2**

-   If you are using the POSIT Cloud (AKA R-Studio online),

    -   Log in and make a new project for lab 2 using [Tutorial 1B](#T1_ProjectsCloud)

-   If you are using R-Studio on your own computer/laptop

    -   Log in and make a new project for lab 2 using [T1_ProjectsDesktop](#T1_ProjectsCloud)
    -   To open/re-open your project, look in the STAT462/Lab2 folder on your computer and double click the .RProj file (I often rename it something like OPENTHIS.RProj)

<br><br>

**[2] Download the lab report template**

-   Go to the Canvas assignment page and, download `Lab1_Template.RmD`,

-   **RENAME IT TO `Lab1_Email_ID.RmD` (e.g. for me, `Lab1_hlg5155.RmD`)** DON'T FORGET THIS STEP!

-   For desktop users, place the file your Lab 2 folder on your computer. On Posit Cloud, open your project, then look for the upload button in the Files tab.

<br><br>

**[4] Edit the yaml code**

-   Inside R-studio, open your lab 2 project (if it's not already open), then click Lab1_Email_ID.RmD to open it. Change the author name at the top to your email ID.

<br><br>

**[5] Check Progress**

-   You should have something like this
    -   e.g. you are in your project, you have downloaded/renamed your lab report and changed the author name. If you are stuck, either go back and redo the tutorials or talk to Dr G.
-   Press knit and check it all works. You might need to install some packages.

<div class="figure" style="text-align: center">
<img src="./index_images/im_Lab02_SetUp.png" alt="*Your screen should look like this*" width="90%" />
<p class="caption">(\#fig:im_Lab02_SetUp)*Your screen should look like this*</p>
</div>

------------------------------------------------------------------------

<br><br>

**[6] OPTIONAL**

If you like my black background or want to change how your code looks as you type, go to the tools menu at the VERY TOP OF THE ENTIRE SCREEN, then click the last option, Global Options. Inside, click appearance.

<br>

### Getting help {.unnumbered}

There are 60 of you and one of me. So we space where you can ask for help, I can answer a question once and you will all be able to see it.

We will do this using the 'github' help discussion boards, as they are then linked to the course Lab book and are designed for code.

Github is a free online system designed for sharing and collaborating on computer code. It is widely used in the professional world

-   **[6]** Go to <https://github.com/> and either make an account or log in. Use any email address.

-   **[7]** Click on the top right to go to your profile, then click edit and add in a few details about yourself or a photo (employers see this, think of it like claiming your LinkedIn page).

<details>

<summary>[Expand to see me do this]{style="color: #1388aa;"}</summary>

```{=html}
   <video width="600" controls>
   <source src="./index_videos/vid_Lab2_GithubSignup.mp4" type="video/mp4">
    Your browser does not support mp4 videos.
   </video>
```
<br>

</details>

-   **[8]** In QUESTION 1 in your lab report, add the web address of your github profile as a clickable link (hint, remember [Visual Mode](#T32A_visualmode).

<br>

-   **[9]** Now go here - <https://github.com/psu-spatial/Stat462-2024/issues> On the right, there is a button called "create an issue". This is what you will click if you have a real question/issue. For now, we will make a test issue. Click "create a new issue", say hello and attach a screenshot of your code (any screenshot is fine).

<br>

------------------------------------------------------------------------

### Functions/Commands and data.frames (spreadsheets) {.unnumbered}

Just read this section. We started by looking at a few commands. Now we will see how these apply to tables of data. Specifically we will be looking at penguins.

The top five things you need to remember

1.  The structure of an R Command is <br> `VARIABLE <- COMMAND(variable_you_apply_it_to, options)`

    1.  So a command/function always has ( ) after it, even if they are empty.

    2.  and you are always saving your answer using the little arrow \<-

        <br>

2.  You can see the help file for ANY command or inbuilt dataset by typing ?commandname into the console e.g. try typing ?mean into the console to see all the possible options, and a worked example at the bottom. I don't recommend typing this into a code chunk as knit gets confused.

    <br>

3.  You must run the library code chunk at the top for anything to work\

    <br>

4.  Within a table, you can select columns using the TableName\$ColumnName (it should autocomplete) e.g. answer \<- mean(mytable\$columnA) will take the mean of column A and save the result to a variable called answer.

    <br>\

5.  You can select within a table/object using SQUARE BRACKETS <br> e.g. TableName[ Row(s) , Column(s)]

<br>



### Penguin data analysis {.unnumbered}

-   **[10]** If you are new to R, consider doing this chapter in data camp - <https://campus.datacamp.com/courses/free-introduction-to-r/chapter-5-data-frames>. It will count for your participation..

#### A. packages {.unnumbered}

Today we will be using commands from several packages. Somewhere near the top of your script, make a new code chunk and add this code. To add a new code chunk, CLICK THE LITTLE GREEN BUTTON (Top Right) and choose the R option.

Before it runs, you might have to install/download the packages first (see [The library tutorial](##T2_Libraries) )



```r
library(tidyverse)
library(skimr)
library(ggplot2)
library(plotly)
library(ggpubr)
library(palmerpenguins)
library(ggstatsplot2)
```

Remember to run the code chunk! [(pressing the green arrow, or go to the run button on the top right and press Run All](https://www.pipinghotdata.com/posts/2020-09-07-introducing-the-rstudio-ide-and-r-markdown/gifs/run-chunk.gif))

Before it runs, you might have to install/download the packages first (see [The library tutorial](##T2_Libraries) )


<br>

------------------------------------------------------------------------
<br>

#### B Load & look at the data

Leave a blank line, and create a new level 1 heading called *Penguin Analysis*. E.g. write the text, click on it, then in visual mode click the little arrow by normal and set to heading 1.

Leave a blank line afterwards too. We're going to work with a table of data that's already pre-loaded into R inside the ggplot2 package.

1.  Make sure you have run the library code chunk above without error, or it won't work. <br>

2.  Load the data using this command. You can ignore the raw penguin data


```r
data("penguins")
```

<br>

3.  Type the `?penguins` command in the console. This will bring up the help file.

4.  State the

-   Object of Analysis
-   A [*reasonable*]{.underline} population you would be happy to apply this dataset to\*
-   Variables and units - you are allowed to copy these names/units from the help file

*\*Imagine you are giving this analysis to a newspaper editor. What population do you think this sample could represent?*

<br>

#### C Examine the data

Now look at the data itself. If you look in the environment tab, you will see a new variable called penguins Click on it's NAME to see the spreadsheet/table itself and familiarise yourself with the data. <br> <br>

We could have also looked at the data by either by typing its name into the console, the command `View(penguins)` or a code chunk, or by using commands like `head(penguins)` to show the first few lines

#### D Examine the data

Let's look at the summary statistics. Leave a blank line and create a new code chunk containing the following code <br><br>


```r
# penguins comes from the palmerpenguins package
# skim comes from the skimr package
skim(penguins)
```

This command compiles the summary statistics for the penguin dataset - sometimes its easier to view this if you press the knit button and look at the html pop-up. You can also use the summary() command to achieve a similar result <br><br>


```r
summary(penguins)
```

Summarise the dataset.

**This should include:**

<br>

1.  A short description of any missing data. For example, are there entire rows missing? Certain columns? Imagine you are using this dataset for modelling, are there rows that will need removing? etc etc? Try \`View(penguins)\` to look at the penguin dataset itself\

<br>
2.  How many penguins were from 2008?


    -   *Hint, [the table command](https://www.statology.org/table-function-in-r/)..*

    -   *Hint 2, to choose a column use the \$ sign e.g. tablename\$columnname*

    -   *Hint 3, R IS CASE SENSITIVE!*\
    
    
    <br>
3.  A histogram of one variable of your choice and a description of the variable.\
    E.g. unimodal? skewed? Any outliers?
    -   \*Hint <https://allisonhorst.github.io/palmerpenguins/articles/examples.html> \*\

<br>
4.  A scatterplot between two variables of your choice and a description of what the data shows.
    -   *Hint <https://allisonhorst.github.io/palmerpenguins/articles/examples.html> \**

    -   \*Hint 2, for a description, [see this Khan page](https://www.khanacademy.org/math/ap-statistics/bivariate-data-ap/scatterplots-correlation/a/describing-scatterplots-form-direction-strength-outliers)\

<br>
5.  The correlation between two variables of your choice
    -   *Hint, [the cor command](https://www.statology.org/r-cor-function/)* \*\

<br><br>



## Submitting your Lab

Remember to save your work throughout and to spell check your writing (next to the save button). Now, press the knit button again. If you have not made any mistakes in the code then R should create a html file in your lab 1 folder which includes your answers. If you look at your lab 1 folder, you should see this there - complete with a very recent time-stamp.

In that folder, double click on the html file. This will open it in your web-browser.\
CHECK THAT THIS IS WHAT YOU WANT TO SUBMIT.

If you are on R studio cloud, see Tutorial 1 for how to download your files

Now go to Canvas and submit BOTH your html and your .Rmd file in Lab 2.



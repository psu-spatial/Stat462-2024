

# R-Markdown {#T3_Markdown}

## What is markdown?  {#T31_Whatisit}

Remind yourself of what Rmarkdown is here <https://rmarkdown.rstudio.com>, or via this short video


```{=html}
<div class="vembedr">
<div>
<iframe class="vimeo-embed" src="https://player.vimeo.com/video/178485416" width="533" height="300" frameborder="0" webkitallowfullscreen="" mozallowfullscreen="" allowfullscreen="" data-external="1"></iframe>
</div>
</div>
```

<br> All markdown documents have three components.

-   There is a space at the top of the file where we can add information about themes/styles etc called "YAML". This determines what type/style of document your work will become <br>
-   There is space to add text (white), <br>
-   And you can add code in 'mini consoles' called 'code chunks'. (Grey) <br>

<img src="./index_images/im_T3_Markdown.png" width="80%" style="display: block; margin: auto;" />


<br>

------------------------------------------------------------------------


## Important things to know {#T32_MarkdownImportant}


### Visual mode {#T32A_visualmode}

It is MUCH easier to edit markdown documents in the new visual mode. Essentially instead of having to remember text short cuts like \* for bold, you can edit the text part as though you were using a word processor. NOTE HEADERS where it says "Normal", this allows you to make auto tables of contents.

![](https://quarto.org/docs/get-started/hello/images/rstudio-source-visual.png)


<br>

------------------------------------------------------------------------



### Inserting images/tables and formatting  {#T32B_formatting}

In visual mode, look at the menu at the top. It's very easy to insert images, tables and other formatting. Pay special attention to the Normal/Heading 1/Heading 2 buttons..

For what I mean by this, see this link: https://zsmith27.github.io/rmarkdown_crash-course/lesson-3-basic-syntax.html 

Note, because of visual mode, you can click a button instead of learning the syntax. 


<br>

------------------------------------------------------------------------

 
### YAML Code and templates  {#T32C_YAML}

For Lab 1 and 2, you will be using a custom template that I made using the package `rmdformats`.[^in_04-tutorial3_markdown-1] This outputs a html file in a special format called 'downcute'.

So for now, don't worry other than editing the author field to include your name

[^in_04-tutorial3_markdown-1]: *You should have downloaded and renamed the lab script from Canvas (see lab 1). You should also be running your project. Click the .RmD file name to open*


<br>

------------------------------------------------------------------------


### Code chunks  {#T32D_CodeChunks}

Code chunks are mini consoles where you can run R commands. We will talk more about them in the next tutorial.

<img src="./index_images/im_T3_CodeChunkCreate.png" width="80%" style="display: block; margin: auto;" />
<br>

On the top right there are a suite of buttons for adding a new code chunk, running code etc. The green one adds a new code chunk. To run an individual code chunk you will press the green arrow on its top right e.g.

<img src="./index_images/im_T3_RunCodeChunk.png" width="90" style="display: block; margin: auto;" />

<br>

------------------------------------------------------------------------

###  Knitting  {#T32E_Knitting}

<img src="./index_images/im_T3_knit.png" width="90" style="display: block; margin: auto;" />

The file on your screen isn't the finished article. To see how it will look as a final version, we need to "knit" it. Go to the top of the .Rmd file, find the `knit` button. Press it (you might have to first save your script if you haven't already, then press it again)

You should see that the Markdown tab "builds" your document and you get an output as a website. The html should also be saved into your project folder.

**Yours will not knit if you haven't yet installed the rmdformats package**

For example, here is a file with markdown and knitted output.

<img src="./index_images/im_T3_AllMarkdownElements.png" width="90" style="display: block; margin: auto;" />

<br> <br>

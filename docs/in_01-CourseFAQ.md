



```{=html}
<style>
details > *:not(summary){
  margin-left: 10em;
}
</style>
```
# Course FAQ {#FAQ .unnumbered}

<br>

## What files should I submit? {#FAQ-1 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

But in general, you need to submit two files; a `.Rmd` file containing your code and a `.html` file for viewing your finished document. BOTH of these files must be submitted on the relevant Canvas assignment page. Occasionally, you might also need to submit your dataset.

This is explained in detail at the end of each lab.

You can also add comments to your submission as needed on the canvas page, or you can message Dr G.

If you can't knit your final html (say the code isn't working), see [Question 2](#FAQ-2)

<br>

</details>

------------------------------------------------------------------------

## My report won't knit! {#FAQ-2 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

Don't panic! This is common. It normally means that you either have an issue with your code or your computer has run out of memory (especially using R-Studio Cloud).

Try these steps to diagnose the issue. Dr G can also help.

1.  Go to the Session menu at the VERY TOP of the screen. Click `Restart-R and clear all output`.
2.  Now go to the environment quadrant and click the little arrow by the pie-chart. Free unused R memory.
3.  Now go back to the Session menu. Click `Restart-R and run all code chunks`
4.  Carefully watch as your code runs. Does it reach the end without any errors or stopping?

<br>

<details id="error">

<summary>[IF YOUR CODE STOPS (There was an error), click here]{style="color: #1388aa;"}</summary>

5.  Read the error message really closely (try reading it out loud) and scroll to the code chunk it's referring to. See if you can fix the issue, starting with the first line that had an error.<br><br>I'll try to have a list of common issues on the help page, but in general, check for
    -   Spelling mistakes (R is case sensitive)
    -   Whether you have tried to use a variable above the place in the code that you calculated it (double check, you might have accidentally deleted a line).
    -   If you are running your project, or it won't be able to find your data/image files.

<br>

<details id="error_change">

<summary>. [If you made a change/fix in your code, click here]{style="color: #1388aa;"}</summary>

6.  Go to the Session menu at the VERY TOP of the screen. Click `Restart-R and run all code chunks`. See if you get to the end.

7.  Keep going, fixing errors as you go, until it all knits. If you still have issues, look at the next section.

<br>

</details>

<br>

<details id="error_nofix">

<summary>. [If you can't find the issue or it still won't knit, click here]{style="color: #1388aa;"}</summary>

6.  Read the error message carefully. See if you can find the problem code chunk(s).
7.  In the top part of any problem code chunks, type eval=FALSE (see screenshot below), then try pressing knit. You might find that you have to stop quite a few code chunks running. This will allow me to see your code and grade what you have.

<img src="./index_images/im_01FAQ_evalFALSE.png" width="650" style="display: block; margin: auto;" />

<br>

</details>

<br><br>

</details>

<br>

<details id="no_error">

<summary>[IF THERE WAS NO ERROR (All the code chunks run with no problems), click here]{style="color: #1388aa;"}</summary>

5.  Make sure you are running your project. Go to the FILES tab. Delete all files EXCEPT your .RProj, your .Rmd, your data and any image files. Basically delete all the auto-created files.
6.  Try pressing knit again.
7.  If it still doesn't work, read the error message carefully and see if it make sense.
8.  If you still have no luck, take a screenshot of the entire screen (including the error message), then ask Dr G for help.

<br><br>

</details>

\
<br><br>

</details>

------------------------------------------------------------------------

## How am I graded? {#FAQ-3 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

You can see the specific rubric I use for each lab on the canvas page.

My grader and I will also provide as much feedback as possible, so please remember to click the "view rubric" button (top right) to take a look.

Overall, here is what your lab should correspond to:

<table class=" lightable-classic-2 table table-striped table-hover table-responsive" style='font-family: "Arial Narrow", "Source Sans Pro", sans-serif; margin-left: auto; margin-right: auto; margin-left: auto; margin-right: auto;'>
<caption>(\#tab:tab-main-rubric)Your overall grade</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> POINTS </th>
   <th style="text-align:left;"> Approx grade </th>
   <th style="text-align:left;"> What it means </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> 98-100 </td>
   <td style="text-align:left;"> A* </td>
   <td style="text-align:left;"> Exceptional.  Above and beyond.   THIS IS HARD TO GET. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 93-98 </td>
   <td style="text-align:left;"> A </td>
   <td style="text-align:left;"> Everything asked for with high quality.   Class example </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 85-93 </td>
   <td style="text-align:left;"> B+/A- </td>
   <td style="text-align:left;"> Solid work but the odd  mistake or missing answer in either the code or interpretation </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 70-85 </td>
   <td style="text-align:left;"> B-/B </td>
   <td style="text-align:left;"> Starting to miss entire/questions sections, or multiple larger mistakes. Still a solid attempt.  </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 60-70 </td>
   <td style="text-align:left;"> C/C+ </td>
   <td style="text-align:left;"> It’s clear you tried and learned something.  Just attending labs will get you this much as we can help you get to this stage </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 40-60 </td>
   <td style="text-align:left;"> D </td>
   <td style="text-align:left;"> You submit a single word AND have reached out to Dr G or Aish for help before the deadline (make sure to comment you did this so we can check) </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 30-40 </td>
   <td style="text-align:left;"> F </td>
   <td style="text-align:left;"> You submit a single word…....  ANYTHING..                Think, that's 30-40 marks towards your total…. </td>
  </tr>
  <tr>
   <td style="text-align:left;"> 0+ </td>
   <td style="text-align:left;"> F </td>
   <td style="text-align:left;"> Didn’t submit, or incredibly limited attempt.  </td>
  </tr>
</tbody>
</table>

<br><br>

</details>

------------------------------------------------------------------------

## I'm late! What's the late policy? {#FAQ-4 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

#### **I rarely incur have late penalties for technical issues.** {.unnumbered}

For example, imagine your code suddenly won't knit. If you send me canvas message with our code and a screenshot of the issue before the deadline, then all late penalties go away until we have fixed it (even if I'm not able to reply immediately).

#### **In general, I prefer you submit late than not at all.** {.unnumbered}

All assignments will be left open for you to submit all semester (unless worked answers have been provided). If you're a few hrs late, you will be absolutely fine, so if you're reading this at 4am, go to bed!

Beyond that, if you're going to be late for any reason then send Dr G a canvas message (you don't need to explain why).

#### [**BUT! Submitting late is a risk.**]{.underline} {.unnumbered}

At any time past the deadline, I reserve the right to:

1.  Release worked answers and close canvas without warning. You cannot submit in that situation as you will already have the answers.

2.  Grade the labs at any time past the deadline without warning. If you miss the grading window, it will probably be several weeks until I am able to give you feedback.

But, I will only start penalizing if you're consistently late and I have sent a written warning, or if I have stated otherwise for an individual assignment. See the course syllabus for more info.

<br><br>

</details>

------------------------------------------------------------------------

## Can I work with friends? What counts as cheating? {#FAQ-5 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

You are encouraged to talk with each other during these labs e.g. you can see each others screens and work out answers together.

**BUT NEVER SHARE CODE OR SEND SCRIPT TO SOMEONE ELSE. ALL TEXT SHOULD BE IN YOUR OWN WORDS.**

For example:

-   Working out together the right way to apply the `seq()` function, then each independently adding it to your own scripts is fine.

-   **Copy/pasting your friend's code/text is never OK**.

So DISCUSS with friends, but then turn away to your own screen and write your own code and text. I will be randomly running lab reports through plagiarism software.

You are also not allowed to get someone else to complete the lab for you, whether online or in person. See the syllabus for the full description.

<br><br>

</details>

------------------------------------------------------------------------

## How can I use chatGPT safely? {#FAQ-6 .unnumbered}

<details>

<summary>[Click here for the answer]{style="color: #1388aa;"}</summary>

<br>

[**This advice is specific to this class.**]{style="color: red;"}

<br>

Your generation is in a weird spot. It’s like when google translate or Wikipedia started. ChatGPT is there, but it’s not yet perfect and society is still working out how it can help and how it can mislead.

[**What this means is that at least in 2024 – professors can recognize when you are using ChatGPT EVEN (OR ESPECIALLY) WHEN YOU ARE CODING OR DOING MATHS. If you imagine coding is like a language, it’s like your handwriting changes.**]{style="color: red;"}

**I'm OK with you using ChatGPT, I use it! Here's how to use it without breaking any rules.**

<br>

Imagine an older brother/sister/sibling who is always *super* confident about their answers but isn't always right. Or if that doesn't work for you, imagine an older friend /undergrad-LA/ friend-who-took-the-course-last-year, or someone on TV.

[Picture them in your mind. I'm going to use my imaginary sister, Sam.]{.underline}

What do I mean?

-   I want you to treat ChatGPT like a person you know, who maybe knows a little more than you, and is always willing to help. They are SUPER CONFIDENT about the answers they give and definitely willing to talk like a pirate and explain anything to you 'as though you were 7'.

-   But! You know that often ChatGPT won't be quite right, their knowledge might be out of date and they might know a different way of getting to the answer than the one you need.

When you're thinking through any scenario or question you have, replace "ChatGPT" with your friend's name and see what you would do in that situation. Here are some scenarios. Scroll to the end to see some example conversations you could try.

<br>

### [**What would Sam do?**]{.underline} {.unnumbered}

<br>

**Plagiarism/cheating..**

-   Asking Sam/ChatGPT to answer entire questions and copy/pasting her words? <br> [Definitely cheating.]{.underline}

-   Getting Sam/ChatGPT to check my grammar and tweak the odd sentence? <br> [Fine!]{.underline}

-   Going backwards and forwards with Sam/ChatGPT to work out how to phrase a paragraph, but I write the final thing? <br> [Fine!]{.underline}

-   Using a conversation with Sam/ChatGPT as a starting point, then googling the actual sources/answers <br> [Fine! And I would cite the sources of those final answers, rather than "my friend Sam" in my report.]{.underline}

-   **Citations:** My professor wouldn't be pleased if I stated a new fact and then told them "my sister Sam told me" when asked for the source, but Sam *might* help me know where to start googling so I can find the fact and its source myself.

<br>

**Authorship**...

-   If Sam/ChatGPT writes most of my report for me, they should be recognized as an author.

-   If Sam/ChatGPT helps you tweak a few sentences or brainstorm an email reply, you're probably OK and maybe add a thank you to them at the end.

<br>

**Coding**...

-   Sam/ChatGPT is quite a good coder. I often show them/copy across my errors and see what they think.

-   But! Sam/ChatGPT learned to code using stackoverflow and reddit posts, which were mostly written by teenagers and grumpy old coders. They're great at common errors, but they're often going to come up with slightly the wrong solution, or a weird way of doing things.

-   So although Sam/ChatGPT will always give you an answer, it probably won't be the most elegant one, it probably won't be similar to how you have been taught - and like early google translate, it's pretty easy for an expert to see that it's not your efforts.

-   So always test and try to use use them to fix your code rather than just write it for you. It is very easy (currently) for professors to see ChatGPT generated code. It's like your handwriting changes. But it's great at debugging your errors.

<br>

**What else is Sam/ChatGPT good & bad at?**

-   Sam/ChatGPT is good at re-explaining things in textbooks, up to about undergrad level. Or ideas which have been around for a long time.

-   Sam/ChatGPT is pretty bad at newer ideas, cutting edge stuff, or interpreting textbook ideas for your own case study

-   It also does better if you are more specific e.g. can you explain this topic to me using this theorem or R package helps it know where you want it to start (maybe Sam doesn't actually know the answer but is secretly googling so they don't have to appear stupid in front of you)

-   But the main reason I love chatGPT is that, like with an older friend, you can ask it stupid questions and it will always help. You don't have to worry about spelling errors writing formally. You can have an actual conversation. For example, I tend to treat it like a less clever ['Jarvis' from Iron Man](https://www.youtube.com/watch?v=D156TfHpE1Q "'Jarvis' from Iron Man") :)

<br>

**Making things up**

-   **ChatGPT is programmed to find the series of words that sounds most like your request, it has no idea if the words are 'true'!** Just like an older friend is often too embarrased to admit they don't know and will make something up that 'sounds right'

-   So Sam/ChatGPT will NEVER say they don't know the answer. Think of the amount of times an overconfident friend/sibling says they definitely know the answer and it turns out to be wrong and they won't even admit it!

-   [Never fully trust what ChatGPT/Sam says! Always google it.]{.underline}

    -   *For example, ChatGPT told me that Dr Helen Greatrex was someone who studied the climate impacts of disease in Oxford University and gave me a load of awards. It was so convincing I had to check I didn't have a name-twin!*

<br>

### [**Example conversation**]{.underline} {.unnumbered}

Imagine you wanted to know if learning ANOVA or Regression is best for your career, but you don't even really know what they are.

Try asking ChatGPT this series of questions :)

-   `Hello! If you have achieved sentience, I hope you are well`

-   `What's the difference between ANOVA and regression?`

-   `I don't get it, can you explain it more simply?`

-   `I still don't get it. Especially this sentence [`*copy paste sentence of your choice*`]. Could you explain that?`

-   `Nope, could you explain it like I'm ten years old and love pirates.`

-   `.........`

-   *..... Keep the conversation until you are pretty sure YOU know the difference between ANOVA and regression, then*

-   `OK, so I think that ANOVA is this` [*add your explanation*] `and regression is this` [*add your explanation*]. `Am I right? Am I missing anything?`

-   `Are there any good textbooks or websites on the topic? (note, it will only know up to 2021)`

    `My career is XXXX. How are ANOVA and regression mostly used in them? Do they use special jargon around this?`

-   `Can you give me concrete examples I can google?`

</details>

------------------------------------------------------------------------

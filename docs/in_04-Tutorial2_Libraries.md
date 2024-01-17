

# Libraries/Packages {#T2_Libraries}

## What are packages? {#T2_Libraries_about}

R is open source, so over the last 20 years, *millions* of useful commands have been written that we might want to use. To make life easier, commands are grouped together into collections called `Packages` or `Libraries` (two names for the same thing). For example, one package might make pretty plots, another might focus on efficient Bayesian analysis.

<br>

------------------------------------------------------------------------


-   ***A close analogy is your phone:** There are millions of apps now available from banking, to social media, to calendars and games.*

-   *But! You don't have every app in the world installed on your phone - Instead you download the apps that you think you will need (occasionally downloading a new one on the fly) -*

-   *You also don't have all the apps you downloaded running at the same time on your phone. When when you need to use an app, you click on it to open.*


Just like your phone, to access the commands in a package we need two steps:

1.  **ONCE ONLY: Download the package from the internet**
2.  **EVERY TIME: Load/Open the packages you want**

------------------------------------------------------------------------

<br>

## Seeing what packages you already have

Some packages are downloaded on your computer by default (just like the flashlight /calculator app on your phone). You can see this list in the Package tab.

<img src="./index_images/im_T2_Packages.png" width="80%" style="display: block; margin: auto;" />

<br>

------------------------------------------------------------------------


## The app store/getting new packages

There is a package for literally everything and there are now well over 20,000 available. You can see the full list here: <https://cran.r-project.org/web/packages/available_packages_by_name.html>

This is far too many to store on your computer, so most live on the internet in an online (free) "Package Store". You can download the ones you want, ready to load later.<br>

<br>

To download/install a new package

### Manually click

This is like going to the app store to get a new app. Just like you only go to the app store once, this is a one-off for each package. NOTE! For R studio cloud online, you might have to do this for each project.

-   Look for the quadrant with the packages tab in it.
    -   You will see a list of packages/apps that have already been installed.
    -   Click the INSTALL button in the Packages tab menu (on the left - see figure above)
    -   Start typing the package name and it will show up (check the include dependencies box). Install the package.
    
<br>

### Little yellow banner

-   R will sometime tell you that you are missing a package (sometimes a little yellow ribbon), click install to install!

<img src="./index_images/im_T2_yellowbanner.png" width="100%" style="display: block; margin: auto;" />

<br>

### Problem solving

#### Why isn't my package downloading? Its frozen

Sometimes R will ask you if you want to install binaries or other things. IT WILL ASK YOU THIS QUESTION THROUGH "SPEAKING" IN THE CONSOLE. It expects you to type yes or no, and to press enter to continue. Try yes, if it doesn't work (esp xfun), try no. <br><br>

#### R keeps asking to restart.

Sometimes R-Studio might want to restart when downloading packages and occasionally gets confused. If it keeps asking, press cancel, then go to the Session menu at the VERY top, click Restart R and Clear output, reopen and try again.

<br>

------------------------------------------------------------------------



## Using/Loading a package you 'own'

Just as going to the app store doesn't check your credit-card balance or make an Instagram post, simply *downloading* a package from the app-store doesn't make the commands immediately available. For that you need to load it (just as you click on a phone app to open it).

**I will tell you which packages you need for each lab, but if R tells you it wants a package, then install it AND load it.**

This can be done with the `library()` command.

For example, this command loads the full works of Shakespeare from the the bardr package. (<https://www.rdocumentation.org/packages/bardr/versions/0.0.9>). If you want to try this, you will need to first install bardr using the instructions above.


```r
library(bardr)
```

<br>

### Using a single command from a package

ADVANCED: Sometimes several packages name a command the same word and you want to specify which package you want to use.

You can do this using the :: symbol. For example, this command *forces* the computer to use the 'dplyr package' version of filter.


```r
dplyr::filter(mydata)
```

<br>

### Problem Solving

#### Nothing happened!

If you have managed to load a package successfully, often nothing happens - this is great! It means it loaded the package without errors.

#### There was a load of text output - an error?

Hard to tell. So I suggest running the library command TWICE! This is because many packages will print "friendly messages" or "welcome text" the first time you load them.

For example, this is what shows up when you install the tidyverse package. The welcome text is indicating the sub-packages that tidyverse downloaded and also that some commands now have a different meaning.

<div class="figure" style="text-align: center">
<img src="./index_images/im_T2_friendlytext.png" alt="Tidyverse install messages" width="100%" />
<p class="caption">(\#fig:im_T2_friendlytext)Tidyverse install messages</p>
</div>

**To find out if what you are seeing is a friendly message or an error, run the command again. If you run it a second time and and nothing happens then you're fine.**

<br>



---
layout: post
title: "Using Sublime Text 2 for R"
date: 2012-05-17T12:00:00-06:00
modified:
author: tom_schenk
categories: blog
excerpt: Run R scripts and open a console with all the benefits of Sublime Text quick text organization tools.
tags: [programming, R, Sublime Text, technology]
share: true
comments: true
---

<figure>
	<img src="/images/r-in-sublime-text2.png" alt="Screenshot of two panes of R source code and a graph created by the R code and was executed within Sublime Text 2.">
	<figcaption>Running R within Sublime Text 2</figcaption>
</figure>

My R interface has been pretty basic in the last few years. I have usually stuck to the R console. Yes, I've tried [Emacs](http://www.gnu.org/software/emacs/) with [ESS](http://ess.r-project.org/); a staple, but it is so unbearably antiquated that I always gave up on its significant learning curve. GUI packages--especially [Rstudio](http://www.rstudio.org/)--offer viable alternatives, but I feel the GUI lets me lose focus of the code[^1]. I have been envious of TextMate for Mac, but alas, I'm not a Mac user. Recently, though, I've moved to [Sublime Text 2](http://www.sublimetext.com/2). With some nudging, I have been able to mimic the typical R console environment in the more-powerful Sublime Text program. 

> Want to skip to the basic instructions without the narrative? Just read the block quotes for specific instructions.

Sublime Text 2 offers a similar experience as TextMate (e.g., autocompleting parenthesis and quotation marks) and integrates well with R and other programming languages. R users aren't the primary target and it takes a little kick to get the environment perfected for the R community. This is a little tutorial to give R users a similar experience with Sublime Text without ruining the program's versatility. That is, you can have a familiar R experience and easily use Sublime Text with programming languages (e.g., JavaScript, C++) and typesetting programs (e.g., LaTeX, Markdown, MultiMarkdown). This setup will let you

*   Browse R code with syntax highlighting
*   Use the familiar R console within Sublime Text
*   Send R code from a script to the R control (equivalent to Ctrl + R)
*   Organizing the layout so the script and console can be viewed simultaneously.

<div>The first and last items are natively supported, but we'll need to make some additional adjustments for the second and third item.</div>

## Initial Setup

> I will presume some user knowledge here and will focus on the Windows user. Setup is very easy. Their website has [links to executable autoinstallers](http://www.sublimetext.com/2 "Install Sublime Text 2"), you won't need to unzip and manual install nor are you depending on a third party to graciously compile code on your behalf.

Follow the instructions and install using the default settings.

## Take a look around

<figure>
	<img src="/images/r-script-syntax.png" alt="An example R script">
</figure>

Before proceeding, take a look at the R interface. Similar to other programs (e.g., [Notepad++](http://notepad-plus-plus.org/)), Sublime Text offers native syntax highlighting for R code. Load one of your codes or try a [sample script](https://gist.github.com/2876877.). If you don't see any highlighting, you can always tell Sublime Text by clicking _View  > Syntax_ and choosing _R_. Otherwise you can look in the lower right-hand corner as is shown in the image. 

<figure>
	<img src="/images/choose-language.png" alt="Choose the R language within Sublime Text">
</figure>

A nifty feature is autocompleting parenthesis and other special characters. Type "_write.csv(_" and it'll auto-insert the right paren "_)_". Little underlines help you match each left parenthesis with the right parenthesis. It also works with "{", "[", single, and double quotation marks. 

<figure>
	<img src="/images/tracking-parenthesis.png" alt="Sublime Text 2 will auto-insert parenthesis">
</figure>

Comments have a lighter tone. So does the ubiquitous "<-". Functions and special characters also have highlighting. If you don't like the color scheme, you can change it under Preferences > Color Scheme. The default is Monokai, Twilight is a very dark theme while iPlastic is a very white theme. 

<figure>
	<img src="/images/autocomplete-variables.png" alt="Once variables are stored, Sublime Text 2 will autocomplete variable names when you type letters.">
</figure>

Once you type a variable or function names, you can easily reference it later for autocompletion. Load the data into a variable called "sampleData" and you only need to type "sa" and hit tab to complete the name. If there are multiple possible matches, then you can use arrow keys to choose. The limitation of this, however, is that Sublime Text treats "sample.data" as two separate names. To counter this, I've started to use underscores, which is friendlier. Also, Sublime Text is using a simple approach--it simply refers to what you've typed before, it is not remembering variables in your memory the same way the GUI interfaces do.

> Click on Preferences > Key Bindings - User, then copy and paste the following (thanks G-Force!)

<script src="https://gist.github.com/tomschenkjr/3050337.js"></script>

There are plenty of shortcuts. Select a few lines of code and press **Ctrl + /** to toggle comments. **Ctrl + L** will select the entire line based on your cursor. **Ctrl + G**, type in a number and you'll jump to that line of code. Type **Ctrl + :** and type a variable name, it'll find all instances. If you have multiple tabs, type **Ctrl + P** and you can jump to specific tabs. At this point, however, you can't execute or "compile" code. It's just pretty font, helpful quirks, and shortcuts.

## **Package Manager**

Our next goal is to be able use the R console and do calculations within Sublime Text. We're going to usethe _SublimeREPL_ package to accomplish this. Don't worry, this isn't a rarefied thing that will clutter your RAM just for R; you'll probably use this package for other things too.

> Visit the [Sublime Package Control website](http://wbond.net/sublime_packages/package_control) and follow the instructions to install the package manager on your computer.

<figure>
	<img src="/images/install-packages.png" alt="Sublime Text 2 package manager can install a command prompt or shell functionality where R can be ran">
</figure>

> To access Package Manager type "**Ctrl + Shift + P**" to bring up a text box. Without using your mouse, begin to type "_Install package_" (without quotation marks). You may see a error related to git.exe, but you can ignore it at the moment. Then type "SublimeREPL" and hit enter when it's highlighted.

SublimeREPL essentially allows Sublime Text to access compilers or other programs. You can write in Sublime Text and send it to R for the computing. The results are sent back to Sublime Text for display. For you, it will operate like the normal R console. However, we need to tell SublimeREPL where R is located on our computer. We need to add R to the Windows Path.

> Find where R is installed. To do this, right click on your R icon--whether it's start menu, desktop, or taskbar. Under the "Shortcut" tab, note the file path under "Target:". Copy and paste this to a text document, you'll need this shortly.

<figure>
	<img src="/images/r-path.png" alt="Add R to the system path so it can be easily discovered when running R commands.">
</figure>

Now,

> Click on _Preferences -> Package Settings > SublimeREPL > Settings – User_. Use the screenshot or example below and paste in the path (thanks Wojciech!).

<figure>
	<img src="/images/editing-path-in-sublime1.png" alt="Add the path of the R directory to the default_extend_env variable in Sublime Text 2.">
</figure>


For example, you might paste: 

<script src="https://gist.github.com/tomschenkjr/2859378.js"></script>

Notice in my example that I am ignoring (disabled) some packages I have installed. In order for this to work, I needed to add a comma after the bracket on line 8 and pasted the "default_extend_env" within the curly brackets. Now you have told where Sublime Text can look to find R.

> Open the R Console by clicking _Tools > SublimeREPL > R_. A window will pop up with the familiar R console header.

<figure>
	<img src="/images/r-console2.png" alt="An open R console from within Sublime Text 2.">
</figure>

## **Further Customization: R Shortcuts**

The R console is fantastic because you can quickly execute code from a script. SublimeREPL does have this capability, but the R user will want to use Ctrl+R, or something similar. Additionally, the native shortcut to execute script has some issues because it conflicts with other shortcuts already built-in Sublime Text. Sublime Text calls these shortcuts "keybindings". Fortunately, they can be edited. However, you have to be careful since Sublime Text has _a lot_ of shortcuts and it's easy to duplicate them, causing further issues. I have a proposed set that should be pretty R user friendly. You can select some code (multiple, partial, or single lines) and run it in R using **Ctrl + Shift + R**. This is similar to the shortcut in the R console (a previous conflict prevents Ctrl + R without a lot of work). To enable new keybindings:

> Go to Preferences > Key Bindings - User and paste the code below. If something if already there, then append the code to the bottom (thanks Wojciech!).

<script src="https://gist.github.com/tomschenkjr/2790415.js"></script>

You can also execute a line of code--without highlighting--using **Ctrl + Alt + R**. Select line(s) of code and send it to the console by typing **Ctrl + Shift + R** and then hitting **R** again. Similarly, display a line of code using **Ctrl + Alt + R** and then typing **R** again. If you want to execute the entire script, type **Shift + F7 **and the entire file will be ran in R, no matter where your cursor is placed. I chose **F7** because that is commonly used to compile code in other languages in Sublime Text. A block of code can be sent by pressing **Ctrl + Alt + Shift + R. ** A block is the code between { }, such as a function. If you want to view the code before it's executed, press **Ctrl + Alt + Shift + R**, then press R again.

## **Side-by-Side**

<figure>
	<img src="/images/side-by-side-view.png" alt="Using Sublime Text's side-by-side view mode to look at R source code and an R console.">
</figure>

It is difficult when the script is in one window and the console in another, but it's easy to have the same feel as the R console.

> To have the script and console side-by-side, click _View > Layout_. Choose either "Columns: 2" or "Rows: 2", depending on your preference. Switch between the side-by-side windows using Ctrl + 1 or Ctrl + 2.

Now you can see your script(s) and output side-by-side.

## **Drawbacks**

The annoyances:

*   The console behaves like a text editor. Your cursor will need to be at the end of the line before you hit enter. Otherwise it just creates a linebreak.
*   When you use Ctrl + Shift + R (send selection) or Ctrl + Alt + R (send line), the console shows ">" every time a command is send. This is a little annoying, but moreso if there are errors in your code.
*   Sometimes the Ctrl + Shift + R or Ctrl + Alt + R is a little finicky, but I think I do it too quickly. Be deliberate if it does not seem to work.
*   When I am doing some heavy R computations, the setup can become slow. It has only happened once and could have ultimately been my fault. Let me know about any performance issues.

Besides R, Sublime Text can also handle other programming/scripting language. It can also handle typesetting languages, such as LaTeX or Markdown. SublimeREPL also works with other languages, such as Ruby and Python.

## **Credits**

This is a tutorial that combines the work of others. This tutorial is just making gumbo from the recipes of others. In particular, [Wojciech Bederski](http://wuub.net/), who wrote the SublimeREPL package, which is key. _Update_: Wojciech also wanted to give props to hootener, who really supported the Windows R implementation for REPL.  [Mads Hartmann Jensen](http://mads379.github.com/) [wrote](https://github.com/mads379/SublimeREPL/commit/1d1527b63fc9abd86ca3bb23dad29dd2604984ac) added the R support in REPL.  Obviously, the Sublime folks have put together a...uh...sublime program.

## Epilogue

[^1]: Since writing this, I've entirely switched my workflow to RStudio. It's development capabilities are fantastic. Nevertheless, Sublime Text 2 has much more advanced editing functionality.
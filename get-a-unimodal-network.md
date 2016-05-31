# Get a unimodal network from a bimodal network

As we saw in the [last tutorial](working-with-selections.md), [bimodal networks](http://www.worldcat.org/oclc/881681427) (e.g., film-actor) can be illuminating, but trying to map relationships between two different entities on the same graph can also lead to confusion. That's why you'll sometimes want to graph unimodal networks instead (e.g., film-film or actor-actor). This tutorial will show you how to get from a bimodal network to a unimodal network.

Take a deep breath and turn on some soothing music, because we're going to do a small amount of programming. I'll take you through each step, though, so you shouldn't ever get lost.

In order to get started with this tutorial, you'll need the following software installed:

* [The R programming language](https://cran.cnr.berkeley.edu/). (Select the type of computer you have, then select the latest version of R, and then download and install the package as you would any software package.)
* [RStudio](https://www.rstudio.com/)[ Deskstop](https://www.rstudio.com/products/rstudio/#Desktop). (Choose the free version.) This is what's called an "integrated development environment" (IDE) for R. RStudio allows you to run your program line by line, and save your work as you go.

You'll also need an edge list. Your edge list can contain as many columns as you want, but the first two columns of the edge list should contain your source and target nodes. If you need help constructing an edge list, or if you don't understand what an edge list is, see [this tutorial](preparing-data-1-making-an-edge-list.md).

If you'd like to practice with a sample two-mode edge list, you can use [this one](edgelist.csv).

## 1. Open RStudio

Open RStudio. You should see a workspace that looks something like the image below. I'm going to spare you much detail about R, the programming language we're using, except to say that it's a language designed for statistical analysis and in wide use among digital humanists. If you'd like to learn more about R, you might look at Matt Jockers's [*Text Analysis with R for Students of Literature*](http://www.worldcat.org/oclc/881681427).

For now, I'll mention just a few things about RStudio, the integrated development environment (IDE) we're using to write our code.

1. The **Console**, on the left-hand side of your workspace, shows the commands you've entered, along with their results.
2. The pane on the upper right-hand side of your workspace shows either the data you've entered into RStudio or the history of your actions (depending on the tab you've clicked).
3. The lower right-hand pane will show you the files on your computer, the visualizations you've created with R, Help documents, or a **Viewer** pane that allows you to see web content (depending on which tab you've selected).

![][1]

[1]: images/get-a-unimodal-network/open-rstudio.png

## 2. Open a new R Script file

We'll open a new, blank file where we can write and save our program. From RStudio's menu, select **File**, then **New File**, and then **R Script**. You should now see a blank document in your workspace, above your console.

Go ahead and click on **File**, **Save**, and give your new document a name, so that you can save your changes.

![][2]

[2]: images/get-a-unimodal-network/open-a-new-r-script-file.png

## 3. Practice entering a command

To run commands in RStudio, you will enter them in the file you just opened, separating each command by pressing **return**.

Let's try running our first command. Type the following into the file you just created:

``
 print("Hello world")
``

Now, with your cursor anywhere on the line you just typed, hold down the **Command** key and press **Return**. (On a Windows computer, hold down the **Ctrl** key and press **Enter**.)

Now look down at the console, which is just below your file. You should see both the command you just entered (in blue) and the result of the command:

``
"Hello world"
``

This is how you'll work in RStudio. Generally, you'll enter one command at a time, run it, and then look down at the console to see the result (and any error messages).

![][3]

[3]: images/get-a-unimodal-network/practice-entering-a-command.png

## 4. Install devtools

Now we'll use RStudio to install devtools, a **package** (add-on) for R that developers use to build and distribute packages that add functionality to R.

To install devtools, type

``
install.packages("devtools")
``

Then place your cursor anywhere on that line and type **command** and then **return** (**control** and **enter** on a PC), just as you did in the previous step. Your console should look something like mine in the image below.

![][4]

[4]: images/get-a-unimodal-network/install-devtools.png

## 5. Install projectoR

Now that we've installed devtools, we'll use it to install a package written especially for us by the great [Matthew Lincoln](http://matthewlincoln.net/)! It's called [projectoR](https://github.com/mdlincoln/projectoR), and Matt wrote it in response to my request for an R program that could simplify the process of projecting a bimodal graph to a unimodal graph. Thanks, Matt!

To install ProjectoR, type

``
devtools::install_github("mdlincoln/projectoR") ``

Now run this command the same way you ran the previous commands.

(Your console won't look exactly like mine because I already had projectoR installed when I ran the command.)

![][5]

[5]: images/get-a-unimodal-network/install-projector.png

## 6. Load projectoR

Even though we've installed projectoR, we haven't loaded it into our current RStudio session. (RStudio only imports packages as you need them, in order to save memory.) Let's tell RStudio that we'll be using projectoR by typing

``
library(projectoR)
``

And, of course, run that line just as you did the previous lines.

![][6]

[6]: images/get-a-unimodal-network/require-projector.png

## 7. Import our data (1)

OK, now we're going to start getting serious. Let's load in our data. We can do that by typing

``
bipartite_list <- data.frame(read.csv(file.choose()))
``

Before we run that command, though, let's look at what it means.

We're creating our very first [**variable**](http://www.programiz.com/r-programming/variable-constant) in R. That variable, called **bipartite_list**, is built by creating a data frame out of a CSV of your choosing. You can tell we're assigning a variable because of that left-pointing arrow. We could've called the variable anything, but I'm calling it bipartite_list because that's what Matt calls it in his documentation.

A [**data frame**](http://www.r-tutor.com/r-introduction/data-frame) is a particular arrangement of data. Technically, it's ["a list of vectors of equal length."](http://www.r-tutor.com/r-introduction/data-frame) What's a **vector**? It's ["a sequence of data elements of the same basic type."](http://www.r-tutor.com/r-introduction/vector) So all of the elements in a vector have to be the same kind of thing: numbers, character strings, or logical values.

Happily, both of the columns in our edge list meet this definition of a **vector**, since they're both composed entirely of character strings. Even better, our edge list is, of necessity, composed of two vectors of the same length -- so it also fits the definition of a data frame.

![][7]

[7]: images/get-a-unimodal-network/import-our-data--1-.png

## 8. Import our data (2)

Now that we've explained what it means, go ahead and run that line of code in the customary way. Mac should launch the file chooser, and you'll be able to navigate to the edge list that you'll be transforming.

(Remember, the first two columns of your edge list should contain your source and target nodes.)

Take a look at the **Environment** pane at the top right of your RStudio workspace. You'll see that it now contains a variable! Every time you create a variable, it'll be listed in that pane. Note that you can click on the variable's name, and even open it up as a table. Handy!

![][8]

[8]: images/get-a-unimodal-network/import-our-data--2-.png

## 9. Convert our two-mode edge list to a one-mode edge list (1)

Time to do what we came to do! We'll accomplish that with one line of code:

``
onemode <- project_table(bipartite_list, joining_col = "films")
``

Before we run this line, though, let's talk about what we're doing here.

When Matt wrote the projectoR package, he [specified a particular function called ](https://github.com/mdlincoln/projectoR/blob/master/R/project_table.R)[**project_table**](https://github.com/mdlincoln/projectoR/blob/master/R/project_table.R). As Matt explains, the project_table function takes two **arguments** (that is, it asks for two pieces of information). The first argument is the name of the data frame that contains the two-mode edge list we want to convert. The second argument is what Matt calls the **joining column**. That is, it's the column that forms the basis of the relationships in the one-mode list you'll create.

To make that more concrete, my two-mode edge list contains two columns: **films** and **actors**. Since I want to make a one-mode edge list that shows how actors are connected to each other, I'll specify that I want to use the other column -- the **films** column -- as the basis of these relationships.

![][9]

[9]: images/get-a-unimodal-network/convert-our-two-mode-edge-list-to-a-one-mode-edge-list--1-.png

## 10. Convert our two-mode edge list to a one-mode edge list (2)

Go ahead and run that command in the customary way. Once you've done that, you should have a new variable, called **onemode**, in the environment pane. If you click on the tiny grid to the right of the variable's name, you'll see that you can even open up our new table in RStudio.

When you open up the onemode table, you'll notice that you have three columns: **from**, **to**, and **weight**. **From** and **to** are pretty straightforward. But what about **weight**?

Weight is an **edge attribute** that describes the strength of the actors' connection, in terms of how many films they've appeared in together. Two actors who appear in one film together will have an edge weight of one, two actors who appear in two films together will have an edge weight of two, and so on.

When you load your new edge list into Cytoscape, you can use the weight to control the visual appearance of your edges.

![][10]

[10]: images/get-a-unimodal-network/convert-our-two-mode-edge-list-to-a-one-mode-edge-list--2-.png

## 11. Save your new edge list to your computer

Now that we've created a data frame called **onemode** that contains the edge list we set out to create, we need to save it to our computer.

Type the following command:

``
     write.csv(onemode, file = "onemode.csv")
``

With this command, we're passing the **function **called [write.csv](https://stat.ethz.ch/R-manual/R-devel/library/utils/html/write.table.html) two arguments: the first, **onemode**, is the name of the file we want to save to our computer; the second, **file = "onemode.csv"**, is the name we want to give to the file we're saving.

To figure out where RStudio, by default, saves files, click on the **Session** menu (in RStudio's main menu), then **Set Working Directory**, and then **Choose Directory**. You don't actually have to choose a directory (unless you want to); just take note of where RStudio's "working directory" -- that is, the first place is goes to look for files and save files. Then press **cancel**.

Now, minimize RStudio and look in your computer's working directory to find your new one-mode edge list, called **onemode.csv**.

![][11]

[11]: images/get-a-unimodal-network/save-your-new-edge-list-to-your-computer.png

## 12. Admire your work

You now have a one-mode edge list that shows you which actors are connected, through a shared appearance in one or more films. Now you can import this edge list into Cytoscape and [build a network diagram](readme.md), just as you did with the previous list.

![][12]

[12]: images/get-a-unimodal-network/admire-your-work.png

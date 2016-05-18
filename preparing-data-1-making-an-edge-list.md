# Preparing Data 1: Making an Edge List

As you learned in [Creating Network Graphs with Cytoscape](readme.md), you need an edge list in order to create a basic network diagam. An edge list generally looks something like this:

| actor | film |
|-------- | ------- |
| Clarence Muse | Heart of Dixie |
| Clarence Muse | Toussaint L'Overture |
| Clarence Muse | The Custard Nine |

At a minimum, an edge list contains two columns. Each row in an edge list describes a relationship. In the case of the list above, each row in the edge list describes *an actor who appeared in a film*.

But if you downloaded a CSV from the "People" table of our database, it probably looks something like this:

LN | FN | AKA | DOB | DOD | Notes | Attachments | Films (Appeared in)
--- | --- | --- | --- | --- | --- | --- | --- |
Muse | Clarence | | 1/7/1889 | | Producer (per Caddoo). General director of Delsarte Film Corp., per GPJ Collection --MP | | Heart of Dixie,Toussaint L'Overture,The Custard Nine |

This tutorial will show you how to get from the spreadsheet you downloaded to a two-column edgelist that you can import into Cytoscape. We will use two pieces of software in order to do this: Microsft Excel (the infamous spreadsheet application) and [OpenRefine](http://openrefine.org/) (a tool for manipulating structured data). If you don't have Excel, you can perform similar operations with [Google Sheets](https://www.google.com/sheets/about/). [OpenRefine](http://openrefine.org/) is a free download for both Mac and Windows computers.

(I won't give you too much detail about OpenRefine in this tutorial, because I'm assuming you want to get to an edge list with a minimum of my commentary. However, OpenRefine is a very useful tool that's worth learning more about. [Here](http://www.meanboyfriend.com/overdue_ideas/wp-content/uploads/2014/11/Introduction-to-OpenRefine-handout-CC-BY.pdf) is my favorite OpenRefine tutorial. If you find you love OpenRefine [I do!], [here is an excellent book](https://www.packtpub.com/big-data-and-business-intelligence/using-openrefine).)

In this tutorial, we'll proceed in several basic steps:

1. Deleting information we don't need.
1. Combining actors' first and last names.
1. Separating film titles into individual cells.
1. Transposing film titles from columns to rows, and filling in blank cells with actor names.

## 1. Delete columns we're not using

Our data will be easier to work with if we get rid of columns we're not going to use in our edge list. Use Excel to open the spreadsheet you downloaded from the database.

If you compare your spreadsheet to the edge list I described aboce, you'll note that the edge list contains only the first and last names of the actors and the titles of the films they've *appeared* in. So we can delete all of the other columns. Do this by clicking on the letter that appears above the column you want to delete, right-clicking or holding down the **Control** key, and choosing **Delete** from the context menu. Using this method, delete columns C-G and I-O. You should have three remaining columns: **LN**, **FN**, and **Films (Appeared In)**.

![][1]

[1]: images/preparing-data-1-making-an-edge-list/delete-columns-we-re-not-using.png

## 2. Create a new column that combines the actors' first and last names

Currently, our actors' names are broken into two parts, to make it easier to alphabetize them by last name. But now we want to combine those two columns, so that we can work with actors' full names in one column.

If your data currently occupies columns **A**, **B**, and **C**, click on cell **D2**, so that a cursor appears in the cell. We're going to type a formula in that cell, so that we can automatically populate every cell in the column with actors' first and last names.

With your cursor in cell D2, type the following formula:

     =CONCATENATE(B2," ",A2)

Thie means: *Take the contents of cell B2, add a space, and join it with the contents of cell A2.*

Press **return**. You should now see the name **Robert Abbott** in cell D2.

![][2]

[2]: images/preparing-data-1-making-an-edge-list/create-a-new-column-that-combines-the-actors--first-and-last-names.png

## 3. Drag the formula into every cell in column D

That's how you'll combine first and last names! Now that you've written a formula that works, let's paste that formula into every cell in column D. Luckily, Excel is smart enough to alter the formula as we go, so that it refers to the data in the appropriate rows.

With cell D2 selected, grab the green square that appears in the lower lefthand corner of the cell. Pull that handle down, so that the formula populates every cell in column D.

![][3]

[3]: images/preparing-data-1-making-an-edge-list/drag-the-formula-into-every-cell-in-column-d.png

## 4. Convert those cells to values

That looks great! We now have a column that contains first and last names. Let's delete columns A and B, so that our data is easier to work with. Unfortunately, we have a small problem: every cell in column D contains a formula that refers to columns A and B. If we try to delete columns A and B, we'll "break" the values in column D.

So let's convert all of the cells in column D to **values**. We'll do that by selecting all of column D (by clicking on the letter **D**). Then **copy** that column by selecting **Edit** and then **Copy** from Excel's menu.

Now comes the tricky part. Select **Edit**, then **Paste Special** from Excel's menu. From the box that pops up, select **Values**, then **OK**. That's it! Now your cells contain values, not formulas.

You can now delete columns **A** and **B** without fear. While you're at it, change the column name **Films (Appeared in)** to simply **Films** and give your column of actors' names the heading **Actors**. That'll make these columns easier to work with later.

![][4]

[4]: images/preparing-data-1-making-an-edge-list/convert-those-cells-to-values.png

## 5. Taking stock

We're getting closer! We now have two columns, one that contains film titles and one the contains actors' names. Unfortunately, many cells in the **Films** column contain multiple film titles, separated with commas.

We need to separate each film title into an individual cell, arrange them so that they all appear in one column, and then tie each film title to the name of an actor.

Save and close your Excel document. We'll complete the next steps in OpenRefine.

![][5]

[5]: images/preparing-data-1-making-an-edge-list/taking-stock.png

## 6. Open OpenRefine and import your spreadsheet

Open OpenRefine by double-clicking it. (Tip: If you double-click OpenRefine and don't see anything, open a web browser and type in the URL `localhost:3333`. This should open OpenRefine in your web browser.)

Click on **Create Project**, then **Choose Files**, then click **Next**.

![][6]

[6]: images/preparing-data-1-making-an-edge-list/open-openrefine-and-import-your-spreadsheet.png

## 7. Inspect your data and create your project

Something about this window makes everyone think that this is where you work with your data, but it's actually just a preview of how your data will look in OpenRefine. Just check to make sure the preview of your data looks OK (it should), and then press **Create Project**.

![][7]

[7]: images/preparing-data-1-making-an-edge-list/inspect-your-data-and-create-your-project.png

## 8. Split multi-valued cells

Now that we're at OpenRefine's main screen, we can separate each film title into its own cell. Do that by clicking on the down arrow to the left of the column title **Films**, then select **Edit columns** and then **Split into several columns**.

In the box that pops up next, make sure that the radio button next to **by separator** is selected and that the **Separator** box contains a common. When you're satisfied, press **OK**.

This instructs OpenRefine to separate each title separated by a comma into its own column. We'll have a lot of columns, but that's OK! We'll deal with them in the next step.

![][8]

[8]: images/preparing-data-1-making-an-edge-list/split-multi-valued-cells.png

## 9. Transpose values across columns into rows

Now every film title is in its own cell, but the cells are spread across multiple columns, instead of neatly packed into one column. We'll squish all these cells into one column using OpenRefine's **Transpose** function.

Click on the down arrow that appears to the left of your first **Films** column. (In my spreadsheet, the **Films** column is the first column.) From the menu that appears, select **Transpose** and then **Transpose cells across columns into rows**.

A somewhat daunting box pops up. We'll work through the options together. In the **From** **Column** option, the **Films 1** column should be selected. In the **To Column** option, your final film column (with my data, it's **Films 24**) should be selected.

From the **Transpose into** options, select **One column** and enter the name **Films** into the text box. Leave **Ignore blank cells** checked, and check the **Fill down in other columns** option.

When your options look like those in the screenshot below, click **Transpose**.

What are we doing here? With all of these selections, we're telling OpenRefine to "melt" all of our many Films columns into a single column, called, simply, **Films**. We're also telling OpenRefine that whenever this "melting" process leaves us with an empty cell in the **Actors** column (which will happen every time one actor appears in multiple films), *fill those Actors cells down* by filling those blank cells in with the value that appears immediately above the empty cells.

If all of this is confusing, don't worry. I've done this about 100 times, and I still have to look up how to do it every time.

![][9]

[9]: images/preparing-data-1-making-an-edge-list/transpose-values-across-columns-into-rows.png

## 10. You have an edge list!

The good news is, you have a dataset that looks like the edge list we examined at the beginning of this tutorial. You should now have two columns, one called **Films** and one called **Actors**.

![][10]

[10]: images/preparing-data-1-making-an-edge-list/you-have-an-edge-list-.png

## 11. Export your edge list

Now let's get our edge list out of OpenRefine, so that we can "feed" it into Cytoscape. Click on **Export** (in the upper right-hand corner) and then choose one of the options. (I like to use **CSV** s when possible, since they're the most generic format. But Cytoscape can read Excel, too.)

OpenRefine will save your fancy new edge list to wherever your browser normally saves downloaded files. Now you're ready to [create a network with Cytoscape](readme.md)!

![][11]

[11]: images/preparing-data-1-making-an-edge-list/export-your-edge-list.png

# Preparing Data 2: Making a Node List from an Edge List

As we learned in the [first Cytoscape](readme.md) tutorial, all you really need to build a network is an edge list. But many times it's nice to have a node list, too: a list of each unique node in your network. If you feed Cytoscape a node list, you can supply extra information about each node, like its type.

For this tutorial, I'm assuming you already have an edge list: a spreadsheet that contains two columns, each row of which describes a relationship between two entities. If you need to learn how to build an edge list for your network, you can learn how to do that [here](preparing-data-1-making-an-edge-list.md). (If you don't have data to work with, you can use [this edge list](data/edgelist.csv) as a starting point.)

In this tutorial, we'll proceed in just a few steps:

1. Selecting each column.
1. Removing all duplicate nodes.
1. Pasting the contents of the second column to the end of the first column.
1. Adding a column that contains "type" information for each node.

## 1. Where we are vs. where we need to be

A node list, as I mentioned, generally looks something like this:

    id | type
    --- | ---
    The Millionaire | film
    The Sport of the Gods | film
    The Gunsaulus Mystery | film
    Robert Abbott | actor
    Mrs. Robert Abbott | actor
    Edward R. Abrahams | actor

In other words, each node is listed *once* in the first column, while the second column (and more columns, if necessary) contain each node's attributes.

Our edge list, on the other hand, looks like this:

     films | actors
     --- | ---
     The Millionaire | Robert Abbott
     The Millionaire | Mrs. Robert Abbott
     The Sport of the Gods | Edward R. Abrahams

Each entity might be listed multiple times, each in the context of a different relationship. Our node list needs to list each entity *once*, and all in the same column. We'll use Excel to do this.

## 2. Select your first column

Click on the **A** above your first column to select every value in Column A.

![][1]

[1]: images/preparing-data-2-making-a-node-list-from-an-edge-list/select-your-first-column.png

## 3. Filter out all duplicate values

From Excel's **Data** tab, select the **Remove Duplicates** option. In the window that pops up, click **Remove Duplicates** again.

![][2]

[2]: images/preparing-data-2-making-a-node-list-from-an-edge-list/filter-out-all-duplicate-values.png

## 4. Repeat steps 2 and 3 for the next column

Easy!

![][3]

[3]: images/preparing-data-2-making-a-node-list-from-an-edge-list/repeat-steps-2-and-3-for-the-next-column.png

## 5. Cut and paste the contents of the second column to the bottom of the first column

You want all the values in a single column. Get rid of the word **Films** first, though. Don't want that in our node list.

![][4]

[4]: images/preparing-data-2-making-a-node-list-from-an-edge-list/cut-and-paste-the-contents-of-the-second-column-to-the-bottom-of-the-first-column.png

## 6. Add a column for type

First, change the name of the first column to **id**. Give the second column the header **type**. Then, in the first cell, type **actor**. With that cell selected, grab the tiny green anchor in the bottom left-hand corner of the cell. Pull that handle down so that the word **actor** appears in every cell in that column that corresponds to an actor in the first column.

![][5]

[5]: images/preparing-data-2-making-a-node-list-from-an-edge-list/add-a-column-for-type.png

## 7. Add film types

For the remaining values in the **id** column, use the same technique to enter the word **film** in the second column.

![][6]

[6]: images/preparing-data-2-making-a-node-list-from-an-edge-list/add-film-types.png

## 8. ...and you're done!

You have a node list! Now you can work with node attributes.

![][7]

[7]: images/preparing-data-2-making-a-node-list-from-an-edge-list/and-you-re-done-.png

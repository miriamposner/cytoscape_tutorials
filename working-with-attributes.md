# Working with Attributes

As we learned in the [last tutorial](readme.md), all Cytoscape *really* needs is an edge list with two columns in it. But you might also want to supply Cytoscape with a list of nodes. That way, you can feed Cytoscape extra information that you can use to distinguish among nodes. That extra information about your nodes is called **attributes**.

(Actually, edges can have attributes, too, as you might have guessed. In the case of edges, the attributes usually describe the nature of the connection between nodes. For example, if I had a People column and a Book column, I could use edge attributes to describe the nature of each connection: *published*, *wrote*, *illustrated*. We'll just deal with node attributes here, but the same steps apply to edge attributes, too.)

## Preparing a node list

Your node list should contain, at a minimum, one column that supplies the name of every node *once*. My edge list, as you may have noticed, contained many actors' names and film titles multiple times. For example, since Ida Anderson appeared in multiple films, I had rows that looked like this:

```
Ida Anderson	Deceit

Ida Anderson	A Son of Satan

Ida Anderson	The Secret Sorrow

Ida Anderson	Gayety

Ida Anderson	Ghost of Tolson's Manor
```

We don't want this in our node list, though. We only want Ida Anderson to appear once, and we only want each film's title to appear once. Actors and films should all be in the same column.

By convention, we usually label node names **id**, although it won't mess anything up if you want to label the column something else.

In subsequent columns, you can provide attributes for each of your nodes. I'll just supply one here, called **type**, containing either **actor** or **film**. You could provide multiple columns, though, like **gender** or **director**.

If you'd like to learn how to construct a node list, you can do that [here](preparing-data-2-making-a-node-list-from-an-edge-list.md).

Once you've prepared your node list, save it as either an Excel document or a CSV (either is fine).

If you'd like, you can use the sample node list located [here](data/nodelist.csv). (This will only work if you also used the sample edge list, though!)

![][1]

[1]: images/working-with-attributes/preparing-a-node-list.png

## Add your node list to your Cytoscape graph

Head back to Cytoscape, where the graph you created during the previous tutorial should be open. We're now going to add our new node list to the existing graph.

Do that by clicking on the **Import Table from File** button, circled below. In the window that pops up, select your node list and click **Open**.

![][2]

[2]: images/working-with-attributes/add-your-node-list-to-your-cytoscape-graph.png

## Check to make sure Cytoscape interpreted your data properly

Hopefully, the window that pops up looks something like the one below. The column labeled with a key is the column Cytoscape will use to try and match your node attributes with the nodes that already exist in your Cytoscape graph.

You can see that Cytoscape has labled your **type** column with an icon that looks like a document. That means that Cytoscape has interpreted that column, correctly, as attribute information for your nodes. This all looks good, so we can click **OK**.

![][3]

[3]: images/working-with-attributes/check-to-make-sure-cytoscape-interpreted-your-data-properly.png

## What happened?

Not a lot, at first glance! But if you look at the pane at the bottom of Cytoscape's window and click on the **Node Table** tab, you'll see that your node table now has an extra column, in which each entity is labeled as either an actor or a film.

That's good! It means the last step worked!

![][4]

[4]: images/working-with-attributes/what-happened-.png

## Use node attributes to color nodes (1)

Now that Cytoscape knows which nodes are which, we can color the nodes based on whether they're an actor or a film. To get started, click on the **Style** tab in the control panel, and make sure the **Node** tab is selected at the bottom of that pane. Your control panel should look something like mine in the image below.

![][5]

[5]: images/working-with-attributes/use-node-attributes-to-color-nodes--1-.png

## Use attributes to color nodes (2)

Remember, the **Map.** column is the one we'll use to color nodes based on their attributes. Click on the **Map.** button in the **Fill Color** row. You should now see some additional options.

For **Column**, choose **type**. (If you included additional attributes in your node list, here's where you could select those as the basis of your nodes' colors.)

For **Mapping Type**, choose **Discrete Mapping**. That means that each node type will receive a different color of your choosing. (Passthrough mapping is for when you've supplied visual attributes, like colors, directly in your node list.) Some properties offer you a Continuous Mapping option. That's for cases when nodes don't differ in type, but in degree -- for example, in cases where you'd like your nodes to increase in size based on how many connections they have. But we're not using that kind of data right now.

Give each type of node a color by clicking on the tiny button that contains three dots. (It appears just the left of the garbage can.) Your graph should change color to reflect your choices.

![][6]

[6]: images/working-with-attributes/use-attributes-to-color-nodes--2-.png

## Using Cytoscape's network analysis tools to calculate attributes

You can supply your own attributes to Cytoscape, as we just did with our node list. However, part of the power of Cytoscape is its ability to calculate certain attributes of your network *for* you. For example, Cytoscape can provide each node with a number that reflects its *degree*, meaning the number of connections to and from that node. We can then use that number to control the size of our nodes.

To get Cytoscape to provide these values, choose **Tools** from Cytoscape's menu, then **Network Analyzer**, then **Network Analysis**, and finally **Analyze Network**. In the window that pops up, Cytoscape will ask you whether you'd like it to treat your edges as directed or undirected. Remember, all of our connections are reciprocal, so select **Treat Network as Undirected**. Once you click **OK**, Cytoscape will perform some calculations, provide you some statistics, and fill in some new columns in your Nodes, Edges, and Network tables.

![][7]

[7]: images/working-with-attributes/using-cytoscape-s-network-analysis-tools-to-calculate-attributes.png

## Understanding these statistics

You can close the Statistics panel, or save the statistics, or both. To understand what these numbers mean, refresh your memory of the [social network analysis glossary](https://github.com/miriamposner/network_analysis_workshop/blob/master/social-network-glossary.md) I provided you in the last tutorial. Here's an important caveat, though: Some of these statistics are meaningful for the kind of graph we have, and some of them aren't. We have a [**bimodal network**](http://www.scottbot.net/HIAL/index.html@p=41158.html), meaning we have two different kinds of things: actors and nodes. Not all measures of networks make sense for bimodal networks.

Degree centrality, for example, still makes some sense for bimodal networks. If a node has a bunch of connections, we know it's either *an actor who appeared in a lot of movies* or *a film that contains a lot of actors*. (Although, obviously, those two qualities are two very different things.) The clustering coefficient statistic, however, means very little for bimodal networks, because your network contains two different orders of things. To read more about measures of bimodal networks, see Scott Weingart's [stern words of advice.](http://www.scottbot.net/HIAL/index.html@p=41158.html)



![][8]

[8]: images/working-with-attributes/understanding-these-statistics.png

## Use your statistics to control the size of nodes

OK! We've calculated some statistics for our nodes, and we've been sternly lectured about the meaning (or lack thereof) of these measures. Let's now (judiciously!) use our measures to control the visual appearance of our network graph.

From your control panel, make sure the **Style** pane is selected, and then make sure the **Nodes** tab is selected at the bottom of the window. This time, click on the **Map.** button for the **Size** property. From the **Column** menu, select **Degree** (because, remember, degree still makes a certain amount of sense for bimodal graphs).

For **Mapping Type**, select **Continuous**. Remember, this means we're distinguishing among our nodes along a spectrum, not breaking them into groups according to type. (We could use Discrete Mapping though! For example, all nodes that have five or fewer connections could be tiny and all nodes that have six or more connections could be big. It just depends on what you want to show.)

You can, if you wish, fiddle with the Continuous Mapping Editor by double-clicking the histogram that appears beneath the Continuous Mapping option. This allows you to control the maximum and minimum size of your nodes, along with the break points, if any.

![][9]

[9]: images/working-with-attributes/use-your-statistics-to-control-the-size-of-nodes.png

## Taking stock

We've done a lot! We've learned how to import a node list; how to use node attributes to control the size, shape, and color of our nodes; how to calculate network statistics; and how to use those statistics to control the appearance of our graph. We can now derive more meaning from the graph we're working with; for example, it's easy, at a glance, to get a sense of which actors appeared in the most films, and which films employed the most actors.

Our graph is still pretty overwhelming for the viewer, though. In the [next tutorial](working-with-selections.md), we'll learn how to work with just parts of it at a time.

![][10]

[10]: images/working-with-attributes/taking-stock.png

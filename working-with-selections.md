# Working with Selections

When we [left off](working-with-attributes.md), we'd learned to build a simple Cytoscape graph, style that graph, import a node list, and use node attributes to control visual elements of our graph. It's much easier now to figure out what's going on in our graph, but it's still a lot to take in.

Sometimes you want to work with smaller chunks of your graph, so you can look at various elements in isolation (or in combination). Some cases when you might want to do this:

* You want to see the [ego network](http://www.analytictech.com/networks/egonet.htm) of a particular node.
* You want to see *only* those nodes or edges that meet a certain criterion: for example, only those nodes that connect to at least three other nodes.

In this tutorial, we'll look at Cytoscape's built-in functions for using various criteria to extract only parts of your graph. I'll assume you've completed the previous two tutorials and have a network with nodes that have attributes of some kind.

## 1. Search for a node

This aspect of Cytoscape is fairly straightforward: If you use the search box to search for a particular node, Cytoscape will automatically highlight it. In this case, Cytoscape is highlighting my node for *The Gunsaulus Mystery*, a 1921 Oscar Micheaux film (lost, alas!).

Perhaps this is obvious, but the yellow highlighting means the node is **selected**.

![][1]

[1]: images/working-with-selections/search-for-a-node.png

## 2. Select the node's neighbors

In many cases, you'll want to select not just a single node, but those nodes that are directly connected to it. Luckily, Cytoscape makes that easy.

Just select the "neighbor-nodes" icon (it looks like two houses) that appears above your network graph.

The result, in my case, is that all of the actors who appeared in *The Gunsaulus Mystery* are highlighted, along with the film itself.

![][2]

[2]: images/working-with-selections/select-the-node-s-neighbors.png

## 3. Extract your selection

We can make our selection easier to see and work with if we extract it from our network diagram. That's just as easy to do as the previous step. Just click the **New Network from Selection** button that's just to the left of the "neighbor-nodes" button.

The result is a new network made just from the nodes you've selected. It stacks on top of your main network graph, and don't worry -- those extracted nodes are still present in your main graph.

![][3]

[3]: images/working-with-selections/extract-your-selection.png

## 4. Selecting from attributes

Cytoscape allows you to select nodes and edges in sophisticated ways. To begin using these capabilities, choose the **Select** pane on the left-hand control panel, and then click the **+** sign to indicate that you'll choose an attribute that you'll use to select nodes.

After you click the **+** sign, you're presented with another of options that you can use to filter. The **column** option allows you to use attributes -- like those you included in your nodes list -- to filter nodes and edges. The **degree** filter is a bit simpler; it allows you to select nodes that meet a certain threshhold for degree centrality. The **topology** filter allows you to select nodes with a certain number of neighbors a certain distance away.

You can stack filters on top of each other, or even chain them together, so that one filter's output becomes the input for the next filter.

We don't have a ton of attributes that make sense as filters, but let's filter our network by **degree**. By setting the degree scrubber to 13, we can select only those films that have at least 13 actors *or* only those actors who have appeared in at least 13 films. We can then extract this sub-network using the same technique we used in **Step 3**.

As you may have gathered, we've gotten to the point where it makes increasingly less sense to work with both films *and* actors in the same graph (which is to say, to work with a bimodal graph). While our bimodal graph is illuminating in certain ways, it's beginning to limit us a bit. As you just saw, for example, degree centrality means two completely different things on our graph -- which means that it's slightly weird to use it as a filtering criterion. Wouldn't it make more sense to show only how *films are connected to each other* or how *actors are connected to each other*?

In order to do this, we'll need to project our bimodal graph into a unimodal graph -- which is what we'll do in the next tutorial.

![][4]

[4]: images/working-with-selections/selecting-from-attributes.png

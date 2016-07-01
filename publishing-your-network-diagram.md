# Publishing your Cytoscape network diagram

So far we've [created a basic Cytoscape network](readme.md), [learned to work with node attributes](working-with-attributes.md), [learned to select parts of a network](working-with-selections.md), and [learned how to convert a bimodal edge list into a unimodal edge list](get-a-unimodal-network.md). Now we'll learn about the ways we can export a network diagram in order to share it with the world.

There are a few different ways to do this, depending on how fancy you want to get. The easiest way is to create a static image of the network. We'll start with that, in Step 1. Creating an [interactive, web-based version](http://goo.gl/j9pgdq) is more fiddly, but not super-complicated. We'll do that second, beginning in Step 2.

## 1. Option 1: Export a static image

You'll be relieved to hear that this is pretty easy. Just click the **Export Network Image to File** button (labeled **1** in the image below). Then -- this is the only confusing part -- press the **Browse** button (labeled **2**) to choose where to save your image. Give your image a name (**3**), then click **OK** (**4**). You can then set the size of the image and a few other parameters, and you'll be able to save the static image to wherever you'd like.

![][1]

[1]: images/publishing-your-network-diagram/option-1--export-a-static-image.png

## 2. Option 2: Exporting an interactive version for the web

This option, alas, has a few more steps, but the result is interactive, zoomable, clickable, and has some other nice features. [Here's an example of one of these interactive network graphs](http://goo.gl/s4BnEu). In broad strokes, you'll:

1. Export your network data from Cytoscape (in a special format called .cyjs);
1. Export the styling you've done to your network (in a special format called .json);
1. Upload the network data to the web;
1. Upload the style information to the web;
1. Enter the URLs to the network and style data to the CyNetShare service;
1. Click visualize!

Here's a hitch: We have to put our files on a server in order to hook them up to CyNetShare. There are a few different ways to do this. If you have access to a server that can host files, that's probably easiest. For the purposes of this tutorial, though, I'm assuming you *don't* have access to a server, so I'll show you how to use Github's [Gist](https://gist.github.com/) service to host your style file.

Hang in there. There are a lot of steps, but none of them is actually that complicated.

![][2]

[2]: images/publishing-your-network-diagram/option-2--exporting-an-interactive-version-for-the-web.png

## 3. Export your network data

Let's export our network data from Cytoscape. To do that, click on **File**, then **Export**, then **Export Network and View**. (Be sure you choose **Network and View**; exporting the network alone won't work.)

For the export file format (**1**), select **Cytoscape.js JSON (*.cyjs)**. In the field labeled **Save Network as **(**2**), click **Browse** (**3**), give your file a name (**4**), and save it somewhere you'll find it again later. Finally, click **OK**.

![][3]

[3]: images/publishing-your-network-diagram/export-your-network-data.png

## 4. Export your style (1)

In the previous step, you exported information about your nodes and edges, but you didn't export any information about the color, size, or layout of your network -- which is to say, you're missing style information.

Luckily, you can export that, too. There are a couple steps involved in this. First, assuming you've been modifying one of Cytoscape's existing styles (that's what we did in previous tutorials in this series), click on the downward-pointing arrow next to the name of the style, and then click **Copy style**. Give your new style a name (it's easiest if you don't use spaces). Then click **OK**.

![][4]

[4]: images/publishing-your-network-diagram/export-your-style--1-.png

## 5. Export your style (2)

Now we can export the style information we just copied. Click on **File**, then **Export**, and then **Styles**. Select the name of the style you created in the previous step. Now -- this is important -- for the export file format, select **Style for cytoscape.js (*.json)**.

Now, just as you did in Step 3, select **Browse**, give your style a name, and save it somewhere you'll remember. Finally, click **Save**, and then **OK**.

![][5]

[5]: images/publishing-your-network-diagram/export-your-style--2-.png

## 6. Create a Gist for your network data

Now we have one file that contains our network data and one file that contains style information. We have to put both of these files on the internet somewhere so that the CyNetShare application, which will host our visualization, can access them. We'll use [Gist](https://gist.github.com/), a service designed to allow people to share code quickly and easily.

In a web browser, go to [gist.github.com](https://gist.github.com/). Now just drag and drop the network file you saved in Step 4 onto the **Add File** box. It will automatically load. Now click on the **Create public gist** button.** **

![][6]

[6]: images/publishing-your-network-diagram/create-a-gist-for-your-network-data.png

## 7. Get the URL for your network data

We want the URL for the raw version of the network data -- meaning the version that doesn't contain all of the Github menus and toolbars -- so click on the **Raw** button.

Now copy the URL for the raw version of your network data. Paste it in a blank document somewhere (or just leave the window open) so you'll be able to find the URL again later.

![][7]

[7]: images/publishing-your-network-diagram/get-the-url-for-your-network-data.png

## 8. Create a Gist for your style information

Now repeat Steps 6 and 7 with the style file you generated in Step 5. Be sure to click on the **Raw** button before you copy the URL.

![][8]

[8]: images/publishing-your-network-diagram/create-a-gist-for-your-style-information.png

## 9. Enter the URLs on CyNetShare

CyNetShare is a website that allows you to publish an interactive version of your network graph. Go to cynetshare.ucsd.edu.

In the **Network Data URL** box, copy and paste the URL to the raw version of the Gist you created to contain your network data.

In the **Visual Style URL** box, copy and paste the URL to the raw version of the Gist you created to contain your style information.

Now click **Visualize!**

![][9]

[9]: images/publishing-your-network-diagram/enter-the-urls-on-cynetshare.png

## 10. Hopefully you have a network!

Hopefully that worked! Ideally, you'll be able to zoom into the network using the scroll wheel (or two fingers) and move the canvas around by clicking, holding for a moment, and dragging.

In practice, I've found that CyNetShare can be a bit buggy. Some things I've encountered:

1. You may have to select your style from the dropdown menu on the top left.
1. If you get a large "loading" image in the middle of your window that won't go away, try clicking on the **Share** button on the right side of the browser window. (It looks like a white arrow on a red background.) Copy the URL that pops up, paste it in a new browser window, and load it. Often that makes the "loading" image go away. (Why? No idea.)

Congrats, you've published your interactive network graph!

![][10]

[10]: images/publishing-your-network-diagram/hopefully-you-have-a-network-.png

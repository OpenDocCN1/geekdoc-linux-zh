# Special Effects

Add a drop shadow to the previous homemade image and you'll see what a difference it can make.

First, select the image that you want to place a shadow behind. For the image you're using here, choose the Fuzzy Select (with Sample Merge activated) on the background, and then choose Select, Invert. If the selection you are working on is part of the background layer, you will need to select Edit, Copy, and then select Edit, Paste to paste into a new transparent layer before adding the shadow.

To make the shadow, right-click on the image and bring up the Layer dialog box. Add another new transparent layer. Name it Shadow. Use the Bucket Fill tool to fill the selected area in the new layer with solid black. Deactivate the selection.

Right-click and select Filters, Blur, Gaussian Blur (either one), and apply a blur strength of about 15 or so. In the Layer dialog, use the Lower Layer button to place the shadow layer under the image layer. Because the shadow is in its own layer, you can use the layer's opacity slider to make the shadow appear paler if you like.

What you will want to do is offset the shadow so that it appears the light source making it over to one side. To do this, right-click and go to Image, Channel Ops, Offset. This brings up an options box where you can choose the amount of offset (pixels) for the X and Y values of the shadow layer. (Remember, X is horizontal and Y is vertical). Positive numbers will offset the shadow to the right for X and down for Y. If you want the shadow up or to the left, enter negative numbers (for example, -8). In Figure 11.6, the drop shadow layer offset is X8, Y8. You can also offset the shadow by moving the layer, but the channel ops give you more control if you want to offset it in an exact amount.

# FIGURE 11.6

The offset to place the shadow in either direction is shown down and to the right from the image itself.

![](bbox=[0.213, 0.663, 0.493, 0.813])

Now you'll work on giving a glow to a selection.

For this, you'll want to begin by following the first steps as you used to create the drop shadow. Place the selection in a transparent layer. Add another transparent layer and
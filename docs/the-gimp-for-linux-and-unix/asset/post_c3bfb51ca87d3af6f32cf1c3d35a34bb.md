
# Layer Techniques

![](img/5164bc49fb24f10213e18cc994b7b40c_196_0.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_196_1.png)

Difference mode. This mode uses channels to subtract colors in the image layer from the blending layer or vice versa, depending upon which layer has the higher brightness.

Addition mode. This mode is similar to Screen mode, but instead of multiplying inverse values, it adds the image and blending layers channel values. The resulting color is always lighter.

# BLENDING MODE EXAMPLES

Subtract mode. This mode subtracts image layer channel values from blending layer values. Subtracting any color with white makes it darker; with black, colors are unchanged.

![](img/5164bc49fb24f10213e18cc994b7b40c_196_2.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_196_3.png)

Darken Only mode. This mode compares image layer and blending layer channel values in order to display the lowest value. Darkening any color with black makes it darker; with white, colors are unchanged.

![](img/5164bc49fb24f10213e18cc994b7b40c_196_4.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_196_5.png)

Lighten Only mode. This mode compares image layer and blending layer channel values in order to display the highest value. Lightening any color with white makes it lighter; with black, colors are unchanged.

Value mode. This mode uses the image layer to determine hue and saturation values and the blending layer to determine value (brightness). Contrast and detail are retained in the image layer.

Hue mode. In this mode, the blending layer's hue is applied to the image layer. The saturation and brightness values of the image layer are not changed.

Saturation mode. In this mode, the blending layer's saturation value is applied to the image layer. The image layer's hue and brightness values are not changed.

Color mode. In this mode, the blending layer's hue and saturation values are applied to the image layer. The image layer's brightness value remains unchanged.

Behind mode. This mode is only used for transparent areas of the blending layer (it's not available in the Layers & Channels dialog box).

# Chapter 11

# Setting Layer Opacity

When working with a layered image, you may want to create a special effect by making one or more layers semi-transparent. This lets the layers below show through. The lower the opacity setting in the Layers & Channels dialog box, the more transparent an image is.

To set layer opacity:

- 1. Right-click on the layered image and choose→Layers & Channels from the pop-up menu (Figure 21). The Layers & Channels dialog box will open (Figure 22).
- 2. Highlight the layer that you want to make transparent.
- 3. Use the Opacity slider to set the transparency of the layer.

![](img/5164bc49fb24f10213e18cc994b7b40c_197_0.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_197_1.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_197_2.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_197_3.png)

# Quick Layer Effects

There are many special effects you can create using layers and GIMP. A few quick ones, including Drop Shadow, Perspective (drop shadow), Round Corners, and Alien Glow, are discussed here.

# Create a drop shadow:

- 1. Use the Layers & Channels dialog box to select which layer will have a drop shadow added to it (for directions about how to do this, turn to page 92) (Figure 23).
- 2. Right-click on the image and choose Script-Fu→Shadow→ Drop Shadow from the pop-up menu (Figure 24). The Script-Fu Drop-Shadow dialog box will open (Figure 25).
- 3. To set where the drop shadow will appear, enter values in pixels in the X and Y offset text boxes. (X offset moves the shadow horizontally, Y offset moves the shadow vertically, thus positive numbers move the shadow right and down, whereas negative numbers move the shadow left and up, respectively.)

![](img/5164bc49fb24f10213e18cc994b7b40c_198_0.png)

Figure 25. Use the Script-Fu Drop-Shadow dialog box to set the offset, size, color, and opacity of the drop shadow. (If this is the first time you are using this feature, try the default settings.)

![](img/5164bc49fb24f10213e18cc994b7b40c_198_1.png)

Figure 26. Use the Script-Fu Color dialog box to set the color of the drop shadow.

(continued)

Figure 27a. This is the original image before the drop shadow is added to the pumpkin layer.

Figure 27b. This is the same image after the drop shadow has been added behind the pumpkin.

![](img/5164bc49fb24f10213e18cc994b7b40c_198_2.png)

- 4. To set how fuzzy the drop shadow is, enter a value in pixels in the Blur Radius text box. The higher the number, the fuzzier the drop shadow.
- 5. Click the color button to open the Script-Fu Color Picker (**Figure 26**).

- 6. Use the Script-Fu Color Picker to set the color of the drop shadow.
- 7. In the Opacity text box, enter a percentage value. The higher the number, the more transparent the drop shadow will be.
- 8. When you have finished setting the various options, click OK. The script-mini-program will go to work and create a drop shadow (**Figures 27a–b**). In addition the Script-Fu Drop-Shadow dialog box will close. Notice that a new layer named “Drop-Shadow” appears in the Layers & Channels dialog box when the drop shadow is created (**Figure 28**).

![](img/5164bc49fb24f10213e18cc994b7b40c_199_0.png)

# To create a drop shadow with perspective:

- 1. Use the Layers & Channels dialog box to select which layer will have a perspective shadow added to it (for directions about how to do this, turn to page 92) (**Figure 29**).
- 2. Right-click on the image and choose Script-Fu→Shadow→ Perspective from the pop-up menu (**Figure 30**). The Script-Fu dialog box will open (**Figure 31**).
- 3. In the text box, enter the value (in degrees) of the shadow.

![](img/5164bc49fb24f10213e18cc994b7b40c_199_1.png)

![](img/5164bc49fb24f10213e18cc994b7b40c_199_2.png)

# Layer Techniques

![](img/5164bc49fb24f10213e18cc994b7b40c_200_0.png)

- 4. To set how long and wide the drop shadow is, enter values in the horizontal and vertical boxes.
- 5. To set how fuzzy the drop shadow is, enter a value in pixels in the Blur Radius text box.
- 6. Click the color button to open the Script-Fu (**Figure 26**).
- 7. Use the Script-Fu Color Picker to set the color of the drop shadow.
- 8. In the Opacity box, enter a percentage value. The lower the more transparent the drop shadow.
- 9. When you have finished setting the various options, click OK. The script-mini-program will go to work and create a drop shadow (**Figures 27a–b**). In addition the Script-Fu dialog box will close. Notice that a new layer named “Perspective” appears in the Layers & Channels dialog box when the drop shadow is created (**Figure 33**).

Figure 32a. This is the original image before the drop shadow is added to the pumpkin layer.

![](img/5164bc49fb24f10213e18cc994b7b40c_200_1.png)

Figure 32b. This is the same image after the drop shadow has been added behind the pumpkin.

![](img/5164bc49fb24f10213e18cc994b7b40c_200_2.png)

Figure 33. When the perspective appears, a new layer.

# PERSPECTIVE SHADOW

# Rounded Corners and a Drop Shadow

It's easy to add rounded corners with a drop shadow to an image using a script-fu.

# To add rounded corners with a drop shadow:

- 1. Use the Layers & Channels dialog box to select the bottommost layer of the image (for directions on how to do this, turn to page 92) (Figure 34).
- 2. Right-click on the image and choose Script-Fu→Decor→Round Corners from the pop-up menu (Figure 35). The Script-Fu dialog box will open (Figure 36).
- 3. In the Radius of Edges text box, enter the value (in degrees) for how much the corners will be rounded. The higher the number, the round corners.
- 4. Select the Add dropshadow check button.
- 5. Use the x and y text boxes to set how the drop shadow is offset from the image (The default setting of 8 for both works perfectly).
- 6. To set how fuzzy the drop shadow is, enter a value in pixels in the Blur Radius text box. The higher the number, the fuzzier the drop shadow.
- 7. If you want the image to have an opaque background color, select the background check button. If this check button is unset, the image will have a transparent background.
- 8. To set the script-fu to work on a copy of the image and keep the original intact, select the Work on copy check button.

![](img/5164bc49fb24f10213e18cc994b7b40c_201_0.png)

Figure 35. Right-click on the image and choose Script-Fu→Decor→Round Corners from the pop-up menu.

![](img/5164bc49fb24f10213e18cc994b7b40c_201_1.png)

Figure 36. Use the Script-Fu Round Corners dialog box to set the size of the rounded corners, add a drop shadow, set the drop shadow offset and blur, and add a background. (If this is the first time you are using these, try the default settings.)

# PAINT TOOLS 675

+   - A double click on the background or foreground field in the toolbox activates the standard color selection dialog. It is worthwhile to experiment with a little with this dialog! Six option buttons allow you to choose between different forms of representing the color layer. The six associated sliders change the hue (H), the saturation (S), and the brightness value (V), together with the intensity of the red (R), green (G), and blue (B) parts.

+   - With DIALOGS | PALETTE or Ctrl+P, you activate a dialog which provides a choice of several predefined color palettes.

+   - If you are working in the INDEXED color mode (the following tip), you can use DIALOGS INDEXED PALETTE to display the available colors in a third color dialog.

+   - Finally, you can use the COLOR PICKER (O) to select the background or foreground color from the image with a click of the mouse.

If work with GIF images, a maximum of 256 colors are available. In the default setting, Gimp always works with RGB colors (2^24) colors, each tints of red, green, and blue. IMAGE | IMAGE | INDEXED can be used to toggle between RGB mode and a limited number of colors. The third available mode is the GRAYSCALE mode with 256 shades of grey.

The color mode has no effect on the appearance of the color selection dialogs. The different paint operations automatically use the most nearly matching color. Please note that in the INDEXED color mode, a number of operations (particularly filters) are not available.

# Blends

The BLEND tool (another name is GRADIENT FILL; keyboard shortcut fills a previously selected area with a continuous transition between two or more colors. For this purpose, the mouse is used to draw an invisible line inside or outside the selection. The colors are applied following the course of this line, the foreground color used for the starting point (and the preceding area) and the background color for the end point. In other words, the direction in which you draw the gradient line matters!

BLEND can only be sensibly employed with selections, which will be discussed only in the next section. Without a selection, the entire image is included, which can at best serve to create a background.

The blend can be controlled by numerous options that can be set in the BLEND toolbox dialog:

+   - The OFFSET ruler controls how soft (0) or hard the blends will look.

+   - The BLEND mode specifies how the colors for the blend are to be mixed. A particularly attractive mode is FG to TRANSPARENT, in which the foreground color is mixed with a transparent color. If you feel that a blend between two
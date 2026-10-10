
![](img/df365d352a104b50fea29e59a052de4d_654_0.png)

When xv starts, it opens only the image display window. Right-clicking anywhere in the window opens the xv controls window. From there, you have access to all of xv's controls. Figure 27.2 shows the xv controls window.

![](img/df365d352a104b50fea29e59a052de4d_654_1.png)

### Note

The main application window is the image display window and not the xv controls window. If you close the image display window, you will close xv—even if the xv controls window is open.

## Using the Menus

The top two rows of buttons in the xv controls window are actually pop-up menus. Clicking one of the buttons will pop up the menu. Releasing the mouse button will close the menu. To select an item in a menu, click the appropriate button, hold the mouse button down, and drag the mouse to the menu item you want. Releasing the mouse button selects that item and executes the appropriate action.

### The Display Menu

The Display menu gives you several options about how (not *where*) to display the image. None of these options actually modifies the image. They only affect how the image is displayed on the screen. Table 27.1 describes each of the options in the Display menu.

| Option | Description |
| :--- | :--- |
| **Raw** | Returns the displayed image to its *raw* state. (That is, the state in which each displayed pixel matches as closely as possible the color of the original pixel in the image.) This option is enabled only after you have issued a Smooth or Dithered command. |
| **Dithered** | If you are running on a PseudoColor display and it is unable to allocate color cells for all the colors in an image, this option will dither the colors in the image, using the colors the display was able to allocate. It has no effect if all the needed colors were obtained or if you are running on a TrueColor display. |
| **Smooth** | Smoothes out distortion caused by integer round-off when an image is resized. Smooth has a useful effect only when the image has been resized. |
| **Read/Write Colors** | Tells xv to use Read/Write color cells, which can help speed up color operations. This option is enabled only when running on a PseudoColor display and the Use Std. Colormap option is not selected. |
| **Normal Colors** | This is the default mode when used on PseudoColor displays. In this mode, xv tries to allocate as many colors from the image as it can. If it runs out of colors, xv tries a few color tricks and then maps the remaining colors to the closest allocated colors. This option is disabled when not running on a PseudoColor display. |
| **Perfect Colors** | This mode first tries to proceed as in the Normal Colors option, but if it fails to allocate any colors, it frees all the colors it allocated and creates its own private colormap. |
| **Use Own Colormap** | This mode causes xv to allocate a private colormap by default. |
| **Use Std. Colormap** | This mode causes xv to use a common colormap for all images being displayed, instead of trying to get all the colors for each image individually. Images might not look as nice in this mode, but it allows you to display several different images simultaneously, without running out of colors. |

### The 24/8 Bit Menu

The 24/8 Bit menu controls the color mode xv operates in: 24-bit color (true color) or 8-bit color (256 colors). When running on an 8-bit (256 color) display, 8-bit mode is the default. When running on a TrueColor display (15-, 16-, 24-, or 32-bit color), 8-bit color is used for image formats such as GIF, in which there can only be up to 256 colors in the image. 24-bit color is used for true color image formats such as JPEG.

One difference between the two modes that can be significant is that in 8-bit mode, xv uses a colormap that can be edited directly. In 24-bit mode, there is no colormap. Also, most of the image editing functions require the image to be in 24-bit mode. If it is not, the image will be converted to 24-bit mode, the editing action will do its work, and then the image will be converted back to 8-bit mode. This can introduce artifacts in the image, so if you plan to use many algorithms, you're probably best off switching xv to 24-bit mode first.

Lock Current Mode keeps xv from changing color modes when a new image is loaded.

The next three options control the method xv will use to convert 24-bit images to 8-bit ones. The fastest one does the worst job of conversion (but it's quick), and the slowest method does the best job. One major difference between the Slow and Best methods is that the Slow method will dither the colors, whereas the Best method will not. The Best method is probably best if you will be enlarging the image much, because the dithering becomes very noticeable as the image is enlarged.

### The Algorithms Menu

The Algorithms menu contains several algorithms that can be applied to an image or a selection within an image. To put it in more common terms, the algorithms are the same as filters in other programs, such as Photoshop. To apply an algorithm to the entire image, you simply select the desired algorithm. To apply an algorithm to a rectangular selection within the image, first select the desired area with the left mouse button, and then select the desired algorithm. Selecting Undo All will undo all algorithms applied to the image, returning it to its original state.

### The Root Menu

The Root menu controls where and how the image is displayed. The two real choices are in a window and in the root window (that is, in the background or on the desktop). If you choose to display the image in the root window, it can be displayed in many different ways. Most of the options simply tile the image in various ways. Root: Centered displays a single copy of the image in the center of the root window. The related warp and brick options act like Root: Centered but also display a warp or brick pattern in the rest of the root window.

![](img/df365d352a104b50fea29e59a052de4d_656_0.png)

## The Windows Menu

From the Windows menu, you gain access to the other windows (and associated functions) available in xv. The Visual Schnauzer is like a simple file manager that enables you to work your way around directories and view their contents, but it also displays thumbnails of images in a directory. Figure 27.3 shows the Visual Schnauzer.

![](img/df365d352a104b50fea29e59a052de4d_657_0.png)

When you first view a directory with the Visual Schnauzer, it will not display thumbnails of any images in the directory until you click the Update button. xv then looks at each file in the directory and, when it finds an image file, xv generates a thumbnail image and saves it in a new file in the hidden directory `.xvpics`. The next time you view this directory, xv will find the `.xvpics` directory and use the already-generated thumbnails when displaying the directory contents. If there are new images in the directory, you must click the Update button again to generate thumbnails for them. If you don't have write permission in the directory you are viewing, xv can still generate thumbnails, but they will not be saved. You will have to regenerate them each time you view that directory.

The Color Editor allows you to perform color and brightness operations on the image. With the Color Editor, you can edit the color palette (if in 8-bit mode), change the hue and saturation of the image, and perform gamma correction for all colors at once (intensity) or for the red, green, and blue channels separately. Figure 27.4 shows the Color Editor.

The Image Info window displays information about the image. The Image Comments window enables you to view any comments saved with an image. Comments do not affect the actual image. They are just added to the header section of the image file. The Text Viewer window enables you to view the image file in ASCII or hex format. If you try to open an image that xv doesn't recognize, it will open it in the Text Viewer window. Figure 27.5 shows the Text Viewer window.

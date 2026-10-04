# Chapter 9. The canvas Widget, Images, and Events

If you don't also use a -scrollregion argument, then the canvas will be xsize by ysize in size, and the entire canvas will be visible.

The -scrollregion command will let you declare that the actual canvas is larger than its visible portion.

For example,

```
canvas .c -width 200 -height 150 -scrollregion {0 0 4500 2000}
creates a window 150 pixels high and 200 pixels wide into a canvas that is actually 4500×2000 pixels.
```

If you attach scrollbars to this canvas, you can scroll this 200x150 pixel window around the larger space.

The -xscrollincrement and -yscrollincrement arguments will let you set how much of the canvas should scroll at a time. For instance, if you are displaying a lot of text in a canvas, you would want to set the -scroll-increment to the height of a line. This will cause the canvas to display full lines of text, instead of displaying partial lines at the top and bottom of the canvas as you scroll through the text.

The next example shows a checkerboard pattern with each square labeled to show its position in the grid. Because the -xscrollincrement is set to the size of a square, the full width of each square is displayed. Because the -yscrollincrement is half the size of a square, half the height of a square can be displayed.

Notice that the -scrollregion can include negative coordinates as well as positive, but you won't be able to scroll to it unless you've set the -scrollregion to include the area you've drawn to.

For example, if you've got a complex image to create and you don't know what the size will be until it's drawn, you can draw the image to a canvas and then determine the bounding box for the image with the command

```
set coords[canvasName bbox all]
```

.
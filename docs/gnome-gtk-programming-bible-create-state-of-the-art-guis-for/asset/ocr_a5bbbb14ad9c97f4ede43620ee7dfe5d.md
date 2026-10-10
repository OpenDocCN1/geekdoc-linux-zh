draw every other segment and the other segments are skipped. Lines 226 through 241 draw a double-dash line by using the foreground and background colors alternately.

You can create dashed lines in any pattern you wish. In this program, the dashed line pattern is defined by the **dashList** array on line 42. Each member of the array specifies a number of pixels to be drawn as the foreground or background. The line drawing routine uses **dashList** to draw 5 pixels, then skip 15 pixels, draw 20 pixels, then skip 30 pixels, and go back to the beginning and skip 5 pixels again, and so on until the end of the line is reached. If you have an odd number of members in the array, the on-off selection is reversed with each pass through the array. For example:

```
char dashList[3] = { 5, 10, 15 };
```

The line begins with 5 drawn pixels, then 10 skipped ones, then 15 drawn, then 5 skipped, then 10 drawn, and so on. It’s just as if the array had six members with the same values duplicated for the last three.

The call to **gdk_gc_set_dashes()** is made on line 207 and has, as its second argument, an index into the array that specifies the starting member—the first line segment to be drawn. The last argument is the number of values in the array.

# Stipple

Using a stippling bitmap gives you bit-by-bit control over which pixels are drawn and which are not. A bitmap is a pixmap with a depth of one—a sort of mask with one bit per pixels that determines which pixels are drawn. A bitmap can be created by using the bitmap utility described in Chapter 7. The bitmap used in the following example is named **stipple.xbm** and, when loaded into the bitmap editor, looks like Figure 11-3.

![](bbox=[0.12, 0.83, 0.42, 0.96])

Figure **11-3**: A bitmap used as a stippling mask
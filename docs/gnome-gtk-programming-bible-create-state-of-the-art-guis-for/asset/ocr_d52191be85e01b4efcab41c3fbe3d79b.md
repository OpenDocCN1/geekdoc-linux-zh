Each letter is a hexadecimal digit. The `gdk_color_parse()` function determines which digits are which by counting the total number of digits in the string (the total must be a multiple of 3). For example, to use two digits per color and specify no red, maximum green, and a little blue:

```
"#00FF3C"
```

On line 57, the `gdk_color_parse()` function returns **TRUE** if the color name is valid. The function `gdk_color_alloc()` is called on line 58 to initialize the color information so it can be used in a graphics context, and the call to `gdk_gc_set_foreground()` on line 59 installs the color into the graphics context as the foreground color. In similar manner, the function calls on lines 61 through 64 establish the background color.

The call to `gdk_gc_set_line_attributes()` on line 67 specifies a *miter join* on a line that is 10 pixels wide. Wide lines are drawn so the details of the line construction can be seen easily. A miter join is one where the outside edges of the lines are extended until they meet. This can work well for shallow angles but, as angles get narrow, the point moves further out and can distort the image you are trying to draw. The call to `gdk_polygon()` on line 72 draws the triangle defined in the array of points defined on line 48. Because we are using the new graphics context, the lines are drawn in blue and are 10 pixels wide. The call to `gdk_draw_string()` on line 77 labels the figure as shown in the upper-left corner of Figure 11-2.

The loop on line 84 moves the triangle points to the next position on the window. The following function calls, on lines 86 through 100, draw another triangle. This time, however, the join style is rounded. This is achieved by having the drawing stop when the line reaches the end point, and then drawing a circle around the end point with a diameter that matches with the edges of the line.

On lines 105 through 119, the triangle is moved to the right once again and drawn with a bevel join. You make a *bevel join* by drawing a straight line between the outer edges of the two lines. This probably is best demonstrated by the 90-degree angle at the bottom—both lines end at the same point and the joint is beveled by filling the little triangle that is left over.

Lines 121 through 186 draw four lines with different ending styles. The *butt ending* draws a square end that includes the pixel at the end points. The *not-last ending* is the same as a butt ending, except the last pixel is not drawn. The *not-first ending* can be used when drawing lines that construct some sort of framework and, because of color differences, the line should not overwritethe pixels of a line already on the display. The *round ending* is simply a circle drawn around the end points. This extends the line beyond each end point by half the width of the line. The *projecting ending* extends the length by half of its width—the same amount as the round ending—and draws a butt ending.

Normally, solid lines are drawn but there are two ways to draw dashed lines. Lines 205 through 224 draw *on-off dashed lines*. That is, the foreground color is used to
The aspect frame container is created in the function makeAspectFrame(), which begins on line 35. The frame widget is constructed on line 42. The first argument is the label that goes at the top of the frame. The second and third arguments are the values xalign and yalign used to position the contained widget—they work here exactly the same as they do for the alignment widget described earlier. In this example, both alignment values are 0.5, which places the contained widget in the middle both horizontally and vertically.

The ratio on line 44 is the ratio resulting from dividing the width by the height. If you want a widget to be four times as wide as it is tall, use the ratio 4/1. If you want the widget to be four times as tall as it is wide, use the ratio 1/4. A ratio number of 1 produces a square widget. Numbers larger than 1 are wide; numbers smaller than 1 are tall.

The last argument, on line 45, is TRUE if the ratio is to be derived from the contained widget or FALSE if the ratio is to be taken from the value passed to it. That is, if you specify TRUE, the ratio value you specify as an argument is ignored and the value from the contained widget is taken. Every widget has a preferred height and width, which implies a preferred aspect ratio.

There are two calls to gtk_container_set_border_width(): the one on line 47 inserts 10 pixels around the outside of the frame and the one on line 51 inserts 10 pixels between the button and the frame.

Figure 5-10 shows the window as it first appears. The overall window size and shape is determined by the aspect ratio, minimum size requirements of the button, and the thickness of the surrounding borders. If the same window is stretched wider while being shrunk vertically, it looks like the window in Figure 5-11. And, if the window is made narrow but longer, it looks like the window in Figure 5-12. The size changes but the aspect remains the same.

![](bbox=[0.13, 0.76, 0.79, 0.88])

You can alter the alignment and ratio information dynamically. To change any or all of the sizing parameters that were established when the aspect frame was created, use a function call like this:

```
gtk_aspect_frame_set(GTK_ASPECT_FRAME(aspect),
                 xalign,yalign,
                 ratio,
                 FALSE);
```
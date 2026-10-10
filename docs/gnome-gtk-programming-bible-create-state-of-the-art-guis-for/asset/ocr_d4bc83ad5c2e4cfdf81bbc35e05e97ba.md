```
70
71    width = event->width;
72    height = event->height;
73
74    return(TRUE);
75 }
76 gint eventDelete(GtkWidget *widget,
77    GdkEvent *event,gpointer data) {
78    return(FALSE);
79 }
80 gint eventDestroy(GtkWidget *widget,
81    GdkEvent *event,gpointer data) {
82    gtk_main_quit();
83    return(0);
84 }
```

Lines 28 through 30 create a drawing area and insert it into the main window of the application. Whenever this main window is resized, the drawing area also is resized. The callback routines are connected to the drawing area on lines 32 through 35. The "expose-event" calls eventDraw() whenever the figure needs to be drawn. The "configure-event" calls Configure() whenever the drawing area changes its height or width.

The rectangles are drawn by the callback function eventDraw() beginning on line 41. The values of xDelta and yDelta, used to size and position the rectangles, are calculated as fractional values of the height and width. The call to gdk_draw_rectangle() on line 46 uses the width and height values to clear the entire drawing area to a white background. Using the fractional values, a black rectangle is drawn on line 52 and a white one is drawn inside it on line 60. Because all dimensions are calculated from the size of the window itself, the figure is drawn to fit. Figure 10-10 shows the appearance of the window in four different sizes and shapes.

![](bbox=[0.18, 0.65, 0.44, 0.83])

**Figure 10-10: Rectangles**

reshaped to fit the window

The callback function eventConfigure() on line 68 is called whenever the window configuration changes. Lines 71 and 73 retrieve the new height and width values and store them until the next time the figure is drawn. There is no need to do anything else because an "expose-event" always follows a "configure-event", and eventDraw() is called to render the figure.
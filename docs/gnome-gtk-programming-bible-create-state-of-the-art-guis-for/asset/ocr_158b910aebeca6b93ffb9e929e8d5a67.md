![](bbox=[0.13, 0.11, 0.38, 0.21])

All of the widgets with the `GTK_FILLER` (designated by “FI” on the display) increased their size until they covered the entire cell. The option `GTK_EXPAND` (“Ex” on the display) did not cause its widgets to expand because `GTK_EXPAND` is really an instruction to the table, not to the widget.

All of these examples apply the same rules to both the vertical and horizontal components of widget space and size. However, with the two arguments, it is possible to set the options in each direction independently of one another. The window can be made homogeneous by changing line 10 to this:

```
#define HOMOGENEOUS TRUE
```

The resulting display, with every cell exactly the same size, is shown in Figure 4-21. When the mouse is used to resize the window, all the cells increase in size by the same amount as shown in Figure 4-22.

![](bbox=[0.13, 0.53, 0.38, 0.59])

![](bbox=[0.13, 0.62, 0.59, 0.73])

The final two arguments are used for padding around a widget. You can create the window in Figure 4-23 by changing lines 10 through 12 to:

```
#define HOMOGENEOUS FALSE
#define X_MARGIN 5
#define Y_MARGIN 10
```

Every widget has 5 pixels added to both its right and left sides, and 10 pixels added to both its top and bottom. This means that the widgets are separated from one
# # Optional Settings

In all the previous examples, the function `gtk_table_attach_defaults()` was used to insert a widget into a table. If you need more control, make the call to `gtk_table_attach()` and override the default settings. These functions both use the same arguments, in the same order, except `gtk_table_attach()` requires four more arguments. The fact is that there is only one function. The function `gtk_table_attach_defaults()` calls `gtk_table_attach()` this way:

```
```c
gtk_table_attach(table,
                widget,
                left_attach,
                right_attach,
                top_attach,
                bottom_attach,
                GTK_EXPAND | GTK_FILL,  /* xoptions */
                GTK_EXPAND | GTK_FILL,  /* yoptions */
                0,                 /* xpadding */
                0);               /* ypadding */
```
```

The last two arguments are the horizontal and vertical padding values—the number pixels that specify either the width or height of a margin around the widget. The specified number pixels are added to both sides of the widget. For example, if you specify a padding value of 5, the overall size is increased by 10.

The `xoptions` and `yoptions` are flags that give instructions to the widget about how to place and size itself within the table cell. The values for this option are listed in Table 4-1. As you can see from the above argument list, the options can cause the widget to act one way vertically and another horizontally. When you mix these options with the *padding*, a table’s grid positioning and homogeneous setting, there are a lot of possible combinations you can use to configure a widget’s display.

**Table 4-1**
**Values of the Table Attach Options**

| Value | Description |
| :--- | :--- |
| 0 | The widget is not resized. It appears at its minimum size. If the containing cell, or cells, is larger than the widget, the widget is centered. |
| GTK_FILL | The widget expands to completely fill the cell, or cells, to which it is assigned. Resizing the table resizes the widget. |
| GTK_SHRINK | If the cell, or cells, containing the widget is smaller than its minimum size, it compresses itself further to fit. |
| GTK_EXPAND | This instructs the table itself to expand to fill any unused space in the window around it. |
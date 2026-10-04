The listbox, text, and canvas widgets support several commands for interacting with the scrollbar. These will be discussed in more detail later in this chapter. An overview of them is as follows:

```
Syntax: widgetName xview options
```

```
Syntax: widgetName yview options
```

xview Change the displayed area of a widget in the X dimension.

yview Change the displayed area of a widget in the Y dimension.

```
Syntax: widgetName yscrollcommand options
```

```
Syntax: widgetName xscrollcommand options
```

yscrollcommand The command to send back to the scrollbar if the widget view shifts in the Y dimension, so that the scrollbar may reflect the state of the display widget.

xscrollcommand The command to send back to the scrollbar if the widget view shifts in the X dimension, so that the scrollbar may reflect the state of the display widget.

The listbox also needs to know that it is associated with a scrollbar. When the listbox changes its display, it will invoke the set subcommand to inform the scrollbar of the change. The set subcommand is supported by the scrollbar to modify the location of the slider.

Also note the -fill option to the pack command. This informs the pack layout manager that this widget should expand to fill the available space and that it should expand in the Y direction. Without this option, the scrollbar would consist of two rows with a 1-pixel-tail bar to use the minimal space.

The equivalent grid option is -sticky ns to tell the grid layout manager that the ends of the widget should stick to top and bottom of the frame.

The following example shows a scrollbar connected with a listbox.
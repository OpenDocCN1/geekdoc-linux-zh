# 8.11 New Windows

```
-resolution .1 -tickinterval 20 -label "Celsius" \
-variable celsius -command celsiusToFahren]

# Pack the widgets.
pack $fahrenscale -side top
pack $celscale -side top
```

# Script Results

![](bbox=[0.305, 0.269, 0.638, 0.432])

# 8.11 New Windows

When the wish interpreter is initialized, it creates a top-level graphics window. This window will be drawn with whatever decorations your display system provides and will expand to fit whatever other widgets are placed within it.

If you find you need another, separate window, one can be created with the tolevel command.

Syntax: tolevel windowName?options?

+   toplevel Creates a new top-level window.

+   windowName The name for the window to create. The name must start with a period and conform to the widget naming conventions.

+   ?options? Valid options for the tolevel widget include:
-borderwidth, -highlightbackground, highlightcolor, -relief, -background, -height, -width.
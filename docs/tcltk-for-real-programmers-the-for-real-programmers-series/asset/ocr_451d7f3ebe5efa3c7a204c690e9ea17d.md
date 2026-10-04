# 9.4 More Canvas Widget Subcommands

```
pack $canv -side top
pack $colorswap -side bottom
```

# Script Results

Before Click

After Click

![](bbox=[0.142, 0.227, 0.477, 0.323])

![](bbox=[0.513, 0.227, 0.848, 0.323])

# 9.4.2 Changing the Display Coordinates of an Item

The previous happy face example simply displayed some graphic items but didn't save the identifiers. The next example creates the happy face and saves the item for one eye to use with the canvas widget subcommand coords. The coords subcommand lets you change the coordinates of a drawable item after the item has been displayed. You can use this to move an item or change an item's shape.

Syntax: canvasName coords tagOrId x1 y1 ... xn yn

+   - coords Return or modify the coordinates of the item.

+   - tagOrId A Tag or unique ID that identifies the item.

+   - x1 y1?... Optional x and y parameters. If these arguments are absent, the current coordinates are returned. If these are present, they will be assigned as the new coordinates for this item.

# Example 9.4.2-1

```
################################################################
# proc wink (canv item) --n# Close and re-open an 'eye' item.
# Arguments
# canv    The canvas that includes this item.
# item    An identifier for the 'eye' to wink
#
# Results
```
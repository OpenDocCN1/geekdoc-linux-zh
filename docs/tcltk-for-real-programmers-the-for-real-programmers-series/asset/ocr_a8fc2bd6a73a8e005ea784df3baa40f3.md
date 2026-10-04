# Chapter 9. The canvas Widget, Images, and Events

```
# winfo returns the geometry of the window within
# its parent as WIDTH+XOFFSET+YOFFSET
# split at the + to separate the X and Y
# offsets.
```

```
# Place the label over the appropriate toolButton
place $labelName -x [expr $x+6] -y [expr $y+10]
```

```
# If this toolButton is close to the right margin
# of the root window, the label won't be
# completely displayed.
# In this case, the label must be moved to the
# left to fit on the window.
```

```
# Update to make the label appear. The $labelName
# geometry is not valid until this update occurs.
update
```

```
# Get the width of the root window, and the width
# of the $labelName label.
# If the X location + width goes over the edge,
# move the label to the left until it fits.
```

```
set rootWidth [index [split [winfo geometry .] "x"] 0]
set labelWidth [index [split \
winfo geometry $labelName] "x"] 0]
```

```
if {[expr $x + $labelWidth] > $rootWidth] {
set x [expr $rootWidth - $labelWidth]
place $labelName -x $x [expr $y+10]
}
```

```
# Save the old event binding, and set a new one,
# that binds a MotionName to destroying the label
```

```
set binding($toolButtonName) \
[bind $toolName <Motion>]
```

316
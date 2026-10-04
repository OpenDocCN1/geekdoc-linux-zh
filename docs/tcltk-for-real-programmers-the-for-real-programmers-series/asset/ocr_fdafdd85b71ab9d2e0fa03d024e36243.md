# Chapter 9. The canvas Widget, Images, and Events

# Converts Y coords for the specified item to center, then
# restores them.
# The item is in its original state when this proc returns.

```
proc wink {canv item} {
    # Get the coordinates for this item, and split them into
    # left, bottom, right and top variables.
    set bounding [$canv coords $item]
    set left [index $bounding 0]
    set bottom [index $bounding 1]
    set right [index $bounding 2]
    set top [index $bounding 3]
    set halfye [expr int($top-$bottom)/2]
    # Loop to close the eye
    for {set i 1} {$i < $halfye} {incr i} {
        $canv coords $item $left [expr $top - $i] $right \
        [expr $bottom + $i];
        after 100
    }
    # Loop to re-open the eye
    for {set i $halfye} {$i >= 0} {incr i -1} {
        $canv coords $item $left [expr $top - $i] \
        [expr $bottom + $i];
        after 100
    }
}
```

# Example Script

```
# Create the canvas and display it.
canvas .c -height 140 -width 140 -background white
pack .c
```

```
# Create a nice big circle, colored gray
.c create oval 7 7 133 133 -outline black -fill gray80 -width 2
```

284
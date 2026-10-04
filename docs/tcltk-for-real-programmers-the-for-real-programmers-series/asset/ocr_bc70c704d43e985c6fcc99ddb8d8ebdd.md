```
#
# Results
# Creates 3 bindings for the item - Enter, Leave, and
# double-click
#
proc setInfo {canv item txt} {
    global highlight background normal
    # display the info text when the item is double-clicked
    $can bind $item <Double-ButtonPress-1> \
        "label .info -text \"$txt\"; grid .info -column 0 -row 1"
    # delete any old info when the cursor enters this item
    # outline this item in highlight color
    $can bind $item <Enter> -catch {destroy .infc};
        .c itemconfigure $item -outline $highlight"

    # return the outline color to normal when the cursor is not
    # over this item.
    $can bind $item <Leave> ".c itemconfigure $item $ \
        -outline $normal"
}

Example Script
set background white
set highlight black
set normal gray75
#
# Create a canvas, and display it
#
canvas .c -height 250 -width 400 -background $background
grid .c -row 0 -column 0 -columnspan 2
#
# Draw the outline of the outside of a rectangular house, and
# define the info for the outside wall.
set house(exterior) [.c create rectangle 8 8 389 248 -width 2 \
    -outline $normal -tag [list exterior wall siding]]
```
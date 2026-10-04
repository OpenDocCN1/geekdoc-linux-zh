
# Results
# Creates 3 bindings for the item - Enter, Leave, and
# double-click

proc setInfo {canv item txt} {
    global highlight background normal
    # display the info text when the item is double-clicked
    $can bind $item <Double-ButtonPress-1> \
        "label .info -text \"$txt\"; grid .info -column 0 -row 1"
    # delete any old info when the cursor enters this item
    # outline this item in highlight color
    $can bind $item <Enter> -catch {destroy .info};
        $can itemconfigure $item -outline $highlight"

    # return the outline color to normal when the cursor is not
    # over this item.
    $can bind $item <Leave> "$can itemconfigure $item \
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

# Chapter 9. The canvas Widget, Images, and Events

```
setInfo .c $house(exterior) \
  "Exterior Wall - white aluminum siding"
```

#
# Draw the outline of the inside of a rectangular house,
# and define the info for the interior walls.

```
set house(interior) [.c create rectangle 11 385 244 \
  -width 11 -outline $normal -tag {interior wall paint}]
```

```
setInfo .c $house(interior) "Interior wall, paint pale green"
```

#
# Create a door for this house.
#

```
set house(frontdoor) [.c create rectangle 220 8 250 11 \
  -fill $normal -outline -tag \
  [list exterior door paint]
```

```
setInfo .c $house(frontdoor) "Outside door, paint blue"
```

#
# And a wall to separate the kitchen from the rest of the house.
#

```
setInfo .c $house(kitchen) "Kitchen wall, paint white"
```

#
# And finally bedroom/bathroom walls
#

```
set house(bed.bath) \
  [.c create polygon \
  250 254 250 255 200 255 200 150 350 150 350 255 \
  255 255 254 \
  -outline $normal -tag [list interior paint] -fill ""
```

```
setInfo .c $house(bed.bath) "Bedroom & Bathroom walls \
  \n paint white"
```

# 9.5 The bind and focus Commands

#
# Make a list of the info tags for this drawing, and bind these
# items to highlight the associated tagged items when the list
# items are entered or left.

```
set ypos 1
foreach l1 [list exterior interior siding paint ] {
  label .l1 -text $l1
  bind .l1 <Enter> ".c itemconfigure $l1 -outline $highlight"
  bind .l1 <Leave> ".c itemconfigure $l1 -outline $normal"
  grid .l1 -row $ypos -column 1
}
incr ypos
```

# Script Results

![](img/fdcc2919568b5b6c9f5301d50a10e8d7_328_0.png)

# 9.5.3 Focus

When a window manager is directing events to a particular item (window, widget, or canvas item), that window is said to have the focus.

# Chapter 9. The canvas Widget, Images, and Events

Some events are always passed to an item that requests them, whether the item is defined as having focus or not. The cursor entering an item always generates an event, and a destroy event will always be transmitted to any applicable item. The keyboard events, however, are delivered only to the widget that currently has the focus.

The window manager controls the top-level focus. The default behavior for MS-Windows systems is to click a window to place the focus in a window. Unix/X Window Systems, the window managers can be set to require a click or to place the focus automatically on the window where resides.

Within the Tcl application, the focus is in the top-level window, unless a widget explicitly demands the focus. Some widgets have default actions that acquire the focus: an entry widget, for instance, takes the focus when you click on it or tab to that widget. If you want to allow KeyPress events to be received in a widget that does not normally gain focus, you must add bindings to demand the focus.

The next example shows a label widget .1 with three events bound to it: Enter, Leave, and KeyPress. When the cursor enters the .1 widget, it acquires the focus, and all KeyPress events will be delivered to the script defined in the bind .1 <KeyPress> command. When the cursor leaves label .1, no events are passed to this item.

The label .12 shares the same -textvariable as label .1. When lvar changes in response to an event on .1, it is reflected in .12. However, .12 never grabs the focus, as .1 does. The bind .12 <KeyPress> (append lvar "L2";) has no effect, since .12 never has focus.

# Example 9.5.3-1

Example Script

```
label .1 -width 40 -textvariable lvar -background gray80
label .12 -width 40 -textvariable lvar

pack .1
pack .12

bind .1 <KeyPress> {append lvar %A;}
bind .1 <Enter> {puts "IN"; focus .1}
bind .1 <Leave> {puts "Out"; focus .}
```

```
bind .1 <KeyPress> {append lvar %A;}
bind .1 <Enter> {puts "IN"; focus .1}
bind .1 <Leave> {puts "Out"; focus .}

# Script Output

```
bind .1 <KeyPress> {append lvar %A;}
bind .1 <Enter> {puts "IN"; focus .1}
bind .1 <Leave> {puts "Out"; focus .}
```

# Script Results

```
bind .1 <KeyPress> {append lvar %A;}
bind .1 <Enter> {puts "IN"; focus .1}
bind .1 <Leave> {puts "Out"; focus .}
```

# 9.6 Creating a Widget

```
bind .1 <KeyPress> {append lvar %A;}
bind .1 <Enter> {puts "IN"; focus .1}
bind .1 <Leave> {puts "Out"; focus .}
```

# Chapter 11. Tk Megawidget

default A numeric value that describes the default button choice for this window. The buttons are numbered from 0.

string The strings to place in the buttons.

# Example

```
tk_dialog .box "Example Dialog" \\
"Who's on first?" \\
questhead 0 "Yes" "No" "Don't Know"
```

![](bbox=[0.425, 0.29, 0.715, 0.363])

+   * tk_megawidget creates a popup menu window at a given location on the display (not constrained within the wish window). The menu appears with a tearoff entry and takes focus. Note that this is not a modal widget. The command after the tk_popup will be evaluated immediately; it will not wait for the user to select an item from this widget.
The following example shows the popup bound to a left button press to display a question based on the contents of a text widget.

**Syntax:** tk_popup menu x y ?entry?

tk_popup Create a popup style menu somewhere on the display. This need not be within the Tcl/Tk application window.

menu A previously defined menu object.

x The x and y coordinates for the menu in screen coordinates.

?entry? A numeric value that defines a position in a menu. The defined position will be selected (active), and the menu will be placed with that entry at the x, y position requested.

# Example

```
proc question {} {
  global var;
```
# 11.1 Standard Dialog Widgets

# Example

tk_optionMenu .button varName Val1 Val2 Val3
pack .button

![](bbox=[0.456, 0.197, 0.523, 0.243])

+   - tk_chooseColor
This color selector widget returns a properly formatted string that can be used for a color name. The string will be the red-blue-green value displayed in the Selection field.
This widget creates a new window in the center of the screen and enables the other widgets in the task that invoked it until interaction with this widget is complete.

Syntax: tk_chooseColor

# Example

tk_chooseColor

![](bbox=[0.298, 0.513, 0.68, 0.658])

+   - tk_getOpenFile
This file browser widget returns the name of a file that already exists. If the user types in a nonexistent file name, an error message dialog box is displayed, and the window focus is returned to the tk_getOpenFile window.
This widget creates a new window on the screen and disables the other widgets in the task that invoked it until interaction with this widget is complete.
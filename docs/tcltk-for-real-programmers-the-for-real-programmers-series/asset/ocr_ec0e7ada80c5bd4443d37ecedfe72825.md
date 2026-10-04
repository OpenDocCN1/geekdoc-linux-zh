# Chapter 11. Tk Megawidgets

Megawidget packages can be created using only Tk or with C language extensions to the wish shell. In this chapter, we'll discuss the megawidgets included with the standard distribution, which are written in Tk, and methods for building your own megawidget libraries with Tk.

# 11.1 Standard Dialog Widgets

Several megawidgets are provided in the Tk 8.0 distribution to simplify writing applications. These widgets extend the functionality of the Tk interpreter and save the script writer from having to reinvent the square wheels.

The implementation of these widgets varies among the platforms Tcl supports. On the Unix platform, they are all implemented as .tcl scripts in the TK_LIBRARY directory. On Windows and Macintosh platforms, some of these widgets are supported by the OS, in which case Tk uses the native implementation. If you prefer to have your application use the Motif-style widgets instead of the native widgets, set the global variable tk_strictMotif to 1, and Tk will use the Unix scripts for these widgets instead of native widgets.

+   - tk_optionMenu

This menbutton widget displays the text of the selected item on the button. The widget creation command returns the name of the menu associated with the button name provided by the script.

```
Syntax: tk_optionMenu buttonName varName val1?val2...valN?
t_optionMenu
```

Create a menu from which to select an item.

A name for the button to be created. This name must not belong to an existing widget. The tk_optionMenu call has returned, this name can be used to display the widget.

The text variable to be associated with the menu. The selected value will be saved in this variable.

The values that a user can select from this menu. These values will be displayed on the button face.
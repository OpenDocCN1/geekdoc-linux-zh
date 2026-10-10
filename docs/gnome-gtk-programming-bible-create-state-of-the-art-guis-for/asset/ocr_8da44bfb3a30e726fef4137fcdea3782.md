On line 26, a call is made to `gtk_signal_connect()` that connects the signal named "`change_orient`" to the applet widget. This is a special signal defined inside `AppletWidget`. It is set to call the function `orientEvent()` whenever the panel changes its orientation. Lines 29 and 30 insert the label into the applet, and put the applet on display in the panel. The "`change_orient`" callback is made when the applet first appears on the panel.

The callback function `orientEvent()` beginning on line 34 changes the text and resizes the label to reflect the current organization. The second argument, the `PanelOrientType`, is used in the switch statement on line 40 to select the orientation. The orientation names refer to the direction from the applet to the root window. That is, `ORIENT_UP` means the applet is on the bottom of the window with the root window above it. `ORIENT_LEFT` means the applet is on the right with the root window to its left.

The size of the label is modified to fit the orientation. If the applet is in a panel at the top or bottom of the screen, the label is widened to accommodate a single line of text. If the applet is on one of the sides, the label is narrowed and the line of text is split.

# ## Summary

An applet is a Gnome with a small main window, and that window appears inside the GNOME panel. An applet derives its special abilities from the `AppletWidget`, which acts as a presentation layer for the applet's main window. This chapter discussed the parts and options, in building an applet:

+   The functions that define and control an applet closely resemble the ones that define and control an application. The function `applet_widget_init()` is used in place of `g_app_init()`. The function `applet_widget_new()` is used in place of `g_app_new()`. The function `applet_widget_gtk_main()` is used in place of `gtk_main()`.

+   An applet can be a mouse-sensitive button that serves as the entrance to a much larger program, but it also can be used to display short messages and simple information.

+   An applet can add any number of members to its menu.

+   An applet can resize and reorient itself to fit with its current environment.

The following chapter explains how you can make inter-process communications available at the GUI interface. The mouse can be used to drag objects from one location to another. The tricks required to package an object and transfer its ownership from one application to another are all built into the GNOME API.
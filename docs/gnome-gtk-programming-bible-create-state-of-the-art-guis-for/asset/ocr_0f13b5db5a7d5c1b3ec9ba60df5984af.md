more than one New option, you should put them on a submenu, as on line 42. In an actual application, only one of these two options should be used.

There is a special menu item defined on line 96. This macro generates the code necessary to create a Help menu, listing the various help topics available for this application. The list of actual topics available is derived from the help files themselves, as described later in this chapter. Figure 8-6 shows the appearance of the menu for an application that has two topics defined in the help files.

![](bbox=[0.13, 0.325, 0.55, 0.46])

Beginning on line 113 is the function that creates the set of menus along with the application's status bar. The menus are created, and attached to the window, on line 117. The status bar is created on line 119, and the call to gnome\_app\_install\_menu\_hints() on line 120 prepares the status bar to display the message found in the menu definitions. The status bar is attached to the application window with the call to gnom\_app\_set\_statusbar() on line 122.

# ## The Help Files

The help files are written in HTML and a browser displays them. To make this work, you place the HTML files—along with an index—into a specific directory. When your application starts running, it reads the topic index file and creates the menu from it.

> In the current version of GNOME, the Netscape Web browser is spawned to display the help text. Future plans are for GNOME to have its own HTML display mechanism designed to work specifically with the help system.

In the previous example, this is achieved on line 96 by using the GNOME\_UI\_INFO\_HELP() macro as part of the help-menu definition. You should include this macro in the help menu always because a menu selection is created only if there is help text defined for the application. Also, the name used is usually the name of the application because these names usually are unique and, hopefully, easy to remember.

Both the program and help file names are stdmain in the previous example. This means the program looks in the following directory for help files:

```
/usr/share/gnome/help/stdmain/C
```
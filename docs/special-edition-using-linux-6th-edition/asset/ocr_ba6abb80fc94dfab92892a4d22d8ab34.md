+   - The Title of Application to Swallow field is the window title of the application. This is usually the title displayed at the top of the window, but if you don’t know it, you can use xwininfo to find out. Run xwininfo from a terminal window and click on the window in question. The title is in the first line of output.
+   - The Command field is the command to run to start this program. If you leave it blank, no command will be run, but as soon as a window with the given title appears (should you run it at start-up, for instance), it will be swallowed.
+   - Finally, the width and height fields are how large to make the swallowed app.
+   - Before creating a swallowed app, you should probably look at the applets list to see whether there is already an applet that does what you want. Applets are more efficient and often provide more features.

**Status dock**—The Status dock holds Status docklets. These are identical to the Dock applets for KDE (such as the CD player and klipper). There are currently no GNOME Status docklets, but the Status dock is compatible with the KDE dock, so you can run KDE Dock applets here.

# USING THE MENU EDITOR

The menu editor modifies the Main Menu. To open the menu editor, click in the main menu, Programs, Settings, Menu Editor. Figure 4.10 shows the Menu Editor window.

![](bbox=[0.26, 0.524, 0.744, 0.816])

Note that some menus are marked User Menus and others are marked System Menus. You can only modify user menus unless you are root.

To open or close a submenu, click the arrow beside its name. To move a menu item from one sub-menu to another, drag it using the mouse. To move it within a sub-menu, right-click and select Move Up or Move Down.
+   1. Right-click in an open space on the panel.
+   2. Select Add to Panel \u2192 Launcher. The Create Launcher window appears.
+   3. Provide the following information for the application that you want to add:
+      * **Name** \u2014 A name to identify the application (this appears in the tool tip when you mouse is over the icon).
+      * **Generic Name** \u2014 A name to identify the type of application.
+      * **Comment** \u2014 A comment describing the application. Like with Name, this information appears when you later move your mouse over the launcher.
+      * **Command** \u2014 The command line that is run when the application is launched. You should use the full path name, plus any required options.
+      * **Type** \u2014 Select Application (to launch an application). (Other selections include Link, to open a Web address in a browser or FSDevice to open a file system.)
+      * **Run in Terminal** \u2014 If it is a character-based or curses application. (Applications written using the curses library run in a Terminal window but offer screen-oriented mouse and keyboard controls.)
+   4. Click the Icon box (it may say No Icon). Select one of the icons shown and click OK. Alternatively, you can browse the Red Hat Linux file system to choose an icon.

> **NOTE:** Icons available to represent your application are contained in the `/usr/share/pixmaps` directory. These icons are either in png or xpm formats. If there isn't an icon in the directory you want to use, create your own and assign it to the application.

+   5. Click OK.

The application should now appear in the panel. Click it to start the application.

# Adding a drawer

By adding a drawer to your GNOME panel, you can add several applets and launchers and have them take up only one slot on your panel. You can use the drawer to show the applets and launchers as though they were being pulled out of a drawer icon on the panel.

To add a drawer to your panel, right-click the panel and then select Add to Panel \u2192 Drawer. The drawer should appear on the panel. The drawer behaves just like a panel. Right-click the drawer area, and add applets or launchers to it as you would to a panel. Click the drawer icon to retract the drawer.

Figure 3-10 shows a portion of the panel that includes an open drawer. This example includes icons for launching a Terminal window, the GIMP, and the Ethereal window.
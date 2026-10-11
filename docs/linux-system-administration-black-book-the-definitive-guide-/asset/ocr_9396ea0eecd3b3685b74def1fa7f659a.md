![](bbox=[0.12, 0.06, 0.78, 0.37])

Figure 6.1 The GNOME Control Center Window Manager.

+   5.  In the Command text box, enter the actual command that has to be run in order to run this window manager. This command is often the lowercased name of the program itself. You can find what you need to type here by looking in the window manager's documentation.

+   6.  In the Configuration Command text box, enter the command that has to be run in order to open the window manager's configuration tool if there is one. Once again, if one is available the command you need to type will be included in the documentation.

+   7.  Click on OK. Now the new item is included among the window managers listed in the Control Center Window Manager.

# ## Adding A Window Manager At The Command Line For GNOME

If you want to try a new window manager for GNOME with your personal account and have already downloaded it, do the following:

+   1.  Log into the account you want to change the window manager for.
+   2.  Type “vi ~/.xintrc” to open or create the local X configuration file.
+   3.  Type “i” to enter vi's insert mode.
+   4.  Type the path for the window manager here. For Enlightenment, this would be “/usr/bin/enlightenment”.
+   5.  Press the Esc key.
+   6.  Type “ZZ” to save and exit.
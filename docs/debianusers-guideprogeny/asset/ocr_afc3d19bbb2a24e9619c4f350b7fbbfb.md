+   3. If necessary, select the Add button to add a window manager to the list. Enter its name and executable.

+   4. Highlight a window manager in the list. Then select the Try button.

+   5. A message window offers you the chance to save the change. If you decide to save the change later, check the Save current setup box as you log out.

+   6. Do one of the following:
+      
+      - Select the Revert button to return to your original window manager.
+      - Select the ok button to continue using the new window manager.
+      
+      If you lose the desktop background image, select Desktop > Background to restore it.

# Changing Window Managers From the Command Line

+   1. Install the window manager packages. You can use the Progeny Debian Window managers package set listed in the Add/Remove Software utility, or install the packages individually.
+      
+      Installed window manager files are generally in a sub-directory of /usr/share, with the executable in /usr/bin or /usr/X11R6.

+   2. Type update-alternatives --config x-window-manager. A list of installed window manager displays.

+   3. Type the number of the window manager you want to use. Then press the Enter key.

# Changing Other Settings

This section explains:

+   - How to change the date and time on your system.
+   - How to change command line shells.
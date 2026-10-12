+   6. Click OK to return to the fonts list.
+   7. Click the **Apply** button at the bottom of the window to make the changes take effect.

# ## Using Added Fonts in OpenOffice

This process will make the fonts available to most KDE- and GNOME-based programs, but they will not be available to all X programs, including OpenOffice. While you probably won't be using OpenOffice on your Red Hat Linux Server very much, I'll tell you how to load the fonts for use there anyway.

+   1. Use the **Run Command** option to open a command window, and enter `opadmin`. Don't be surprised if it takes a few moments for the OpenOffice printer administration tool to load.
+   2. When it does, click the **Fonts** button to list the installed fonts.
+   3. Click the **Add** button to add the new font directory.
+   4. Click the `...` button to open the graphical representation of the system's directory structure.
+   5. Find the correct parent directory and type **.fonts** after it (files and directories that start with a period are “hidden,” so you won't be able to select the **.fonts** directory from the list).
+   6. Click **Select All** to select all the fonts in the directory.

![](bbox=[0.25, 0.56, 0.71, 0.8])

+   7. Click **OK** to add all the selected fonts.
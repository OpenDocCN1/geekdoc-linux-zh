of the script to point to the directory where the various Briscola files are located. To perform the adjustments as instructed in the README file, just follow these steps:

+   Open a Console window and find the Tk shell, called Wish, by typing **locate wish**; press ENTER and then note on a piece of paper the location given.
+   
+   Now right-click the *briscola.tk* file itself in the briscola folder, and select **Open With ▶ Text Editor** in the pop-up menu.
+   
+   When the briscola.tk file opens within Text Editor, change the very first line from `#!/usr/local/bin/wish` to `#!/usr/bin/wish`, which should have been the location given as the result to your *locate* search in step 1. The `#!` at the beginning of the line, in case you’re wondering, indicates the path to a shell, in this case the Tk shell.
+   
+   Now, in the second line, change `/usr/local/games/briscola/` to `/usr/local/share/games/briscola/`, which is where you are going to be placing the briscola folder so that all of the users on your computer can play it.
+   
+   Once you have done this, go to the Text Editor **File** menu and select **Save**.
+   
+   Quit Text Editor.

# **20B-4: Moving the Briscola Folder to a Global Location**

If you’re leaving the briscola folder where it is now (in your Home folder), only you would be able to play the game. To make it available to others who have user accounts on your machine, you need to copy it to a global location. Since global locations are all in root territory, you will first have to become root before you do any copying. Here’s what to do:

+   Open a Console window (if one isn’t open already), and become root by typing **su** and pressing ENTER.
+   
+   When prompted for your root password, type it in and press ENTER.
+   
+   Copy the briscola folder to its new global locations by typing `cp -r briscola /usr/local/share/games`. Then press ENTER.
+   
+   Exit root mode by typing **exit** and pressing ENTER.

# **20B-5: Running Briscola**

You can now run Briscola (and double-check your work) by doing the following:

+   In the Console window, move into the new globally located briscola folder by typing `cd /usr/local/share/games/briscola` and pressing ENTER.
+   
+   Now run Briscola by typing `./briscola.tk` and pressing ENTER.

> NOTE  In case you were wondering (since there is no *briscola.tk* command), your system doesn’t know what to do with your input. The ./ that you typed in step 2 tells your system to run the script you have signified after the slash (briscola.tk).
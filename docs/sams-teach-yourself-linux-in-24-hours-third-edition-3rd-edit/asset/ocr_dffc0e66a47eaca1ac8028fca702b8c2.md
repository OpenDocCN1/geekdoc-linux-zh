+   3. Use the switchdesk command to change to another desktop environment. Use the directions at the end of Appendix A.
+   
+   4. When you are back in a desktop environment, look for the following file in your home directory and open it in your favorite text editor:
+   `.Xclients-localhost.localdomain:0`
+   
+   5. Comment out each line in the file. Place a # character (the comment out character) in front of the execution command for your current desktop environment. (An example is shown in Figure 19.2.) You might see one of these two lines:
+   `exec startkde`
+   `exec gnome-session`
+   
+   6. Type the script for the window manager that you want to use at the end of the file. To use AfterStep, type the following:
+   `exec /usr/X11R6/bin/afterstep`
+   Your file will look like the one in Figure 19.3.
+   
+   7. Save the file and close it.
+   
+   8. Restart the X session. Log out of the account. When you are back at the text-only console, type `startx` and press Enter. You'll see the AfterStep desktop shown in Figure 19.4.

# FIGURE 19.2
Comment out the execution command.

![](bbox=[0.24, 0.44, 0.79, 0.79])

Doing this will comment out the line, and the server will not read it when it next reads the .Xclient script file.
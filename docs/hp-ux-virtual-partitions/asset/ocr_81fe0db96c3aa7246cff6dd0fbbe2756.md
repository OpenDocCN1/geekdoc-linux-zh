As with front panel control buttons, it's easier to copy and modify an existing subpanel file than to start from scratch.

# Changing the Default Printer Name Display

We'll now make an easy change to one of the slide-up subpanels. If we pop up the Personal Printers subpanel, it shows that we have a default printer configured, but not the name of it. Let's go back into the front panel file, dtwm.fp, and change that:

+   1.  Bring up your favorite editor, such as *dtpad* or *vi*, and edit the file $/HOME/di/types/dtwm.fp.
+       2.  Scroll down to CONTROL Printer. You'll see that the LABEL is Default. Change or add to that the name of your default printer. My printer is called a464.
+       LABEL     Default - a464
+       3.  Save the file and restart the Workspace Manager. Position the mouse over a blank area on your workspace and press the right mouse button. Select Restart Workspace Manager. On Solaris, press the right mouse button to bring up the Customized Workspace Menu. From here, select Windows, where you'll find the Restart Workspace Manager key.

Pop up the Personal Printers subpanel to see what the default printer really is. Of course, if we change the default, we'll have to change the front panel again. But we know how to do that now, don't we! Figure 14-8 shows the Front Panel.
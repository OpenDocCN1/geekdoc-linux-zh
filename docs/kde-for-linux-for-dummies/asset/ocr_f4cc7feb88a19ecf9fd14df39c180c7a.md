+   3. Click **OK**.
+   	Do not click **Apply**. If the new setting doesn't seem to work, redo this procedure and make sure you click **OK** instead of **Apply**.

If it still doesn't work, you can do some heavy-duty mangling to get your program working properly. Making your program work correctly involves hands-on Linux work, so if you're uncomfortable with doing such things, take a deep breath and promise yourself ice cream afterward.

Open your file manager and locate the following directory:

```
opt/kde/share/apps/kdisplay/app-defaults
```

Phew! That's a mouseful. After you locate the directory, you need to either delete or rename the directory. Doing this keeps the X Window System from locating the default Kdisplay resource files (the ones that the X Window System uses to assert KDE styles over the non-KDE application's defaults).

![](bbox=[0.1, 0.45, 0.2, 0.56])

In cases where you have the option to either delete or rename a file or directory, you're almost always making the better choice to rename the file or directory (and to make a note of both its original name and the one you used for renaming). In the event that you need to put the file back, you still have it. If the file's deleted, you may have to go all the way and reinstall from scratch. Renaming saves time.

After you rename or delete the directory, log out of your user account and then log back in. Logging out causes X to restart and allows the non-KDE program to use its own settings.

# Okay... but It's Still Not Working

If you have different problems than the ones noted above, or if these tricks still aren't getting your problem solved, you may want to find an expert somewhere. Consult Chapter 16 and Appendix B to find places where KDE-savvy people hang out on the Internet. Chances are, if you're experiencing problems with a popular non-KDE application, you are not the first one to find the KDE feature that's holding you back.

You may also want to check out the non-KDE application's Web site to see if there are known conflicts with KDE. Sometimes all you have to do is download and install a bug patch.
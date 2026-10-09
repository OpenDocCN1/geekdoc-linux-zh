where to locate this launcher's entry in the menu system.

+   5) Click **Apply**, then **Close**.

Now go to **Main Menu > Applications > Accessories**, where you will see that '**Nautilus as Root**' has been added to the menu. Click on this entry and Nautilus will run, though it is not quite the same Nautilus as before. For example, the bookmarks you created earlier have disappeared, and if you had set any preferences (in *Edit > Preferences*) these will have gone too. It is in fact a different instance of Nautilus.

The (**ROOT**) terminal that you can run from here will also be a different instance of Terminal, with different preferences. Test this out now:

+   1) Right-click on an empty space in the Nautilus window, and choose '**Open in Terminal**'. Terminal as **Root** opens, but with awkward colours.

+   2) To fix these colours, open Terminal's *Edit menu* and choose '**Profile Preferences**'. Open the *Colours* tab, then untick the '**Use colours from system theme**' box. At '**Built-in scheme**', choose **Custom**. Now set the background colour to something like dark red; this will serve as a warning when you are in this instance of Terminal that you are in superuser mode.

+   3) Click **Close**, then close Terminal but keep Nautilus as **Root** open in preparation for the next section.

# 2.8 Customizing the Nautilus Icon

It should be an easy task to replace the rather dull-looking icon that's been assigned to Nautilus, but there appear to be two missing icons folders in the **Enlightenment** file system that prevents us doing so. Furthermore, these folders are in a protected part of the system, which means we can't create them by running Nautilus in the normal way, instead we must run it as **Root**.

+   1) If Nautilus as **Root** is not already open, open it now (*Main menu > Accessories > Nautilus as Root*).

+   2) Navigate to `/usr/local/share`, right-click on an empty part of the folder window and choose '**Create new Folder**'. Enter `icons` as the name.

+   3) Navigate to `/usr/share/enlightenment` and create an `icons` folder here too.

+   4) Having created the two missing folders, you can close Nautilus as **Root**. Instead you should now run it normally (by double-clicking its icon on the desktop).

To change its icon, proceed as follows:

+   1) Right-click on the orange Nautilus title bar and choose **Nautilus > Edit Icon**.
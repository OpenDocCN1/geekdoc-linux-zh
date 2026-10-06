# 104 Part I ◆ Linux First Steps

From Gnome's Panel menu, you can choose from a variety of functions, including:

+   * **Use menus**— The Applications menu displays most of the applications and system tools you will use from the desktop. Places menu lets you select places to go, such as the Desktop folder, home folder, removable media, or network locations. The Desktop menu lets you change preferences and system settings, as well as get more information about GNOME.
* **Add to Panel**— Add an applet, menu, launcher, drawer, or button.
* **Delete this Panel**— Delete the current panel.
* **Properties**— Change the panel's position, size, and background properties.
* **New Panel**— Add panels to your desktop in different styles and locations.

You can work with items on a panel. For example, you can:

+   * **Move items**— Move items on a panel simply by dragging and dropping them to new positions.
* **Resize items**— Some elements, such as the Window List, can be resized by clicking an edge and dragging it to the new.
* **Use the Window List**— Tasks running on the desktop appear in the Window List area. Click a task to minimize or maximize it.

The following sections describe some things you can do with the GNOME panel.

# The Applications and Desktop Menu
On the panel, you see categories of applications and system tools that you can select. Click the application you want to launch. To add an item to launch from the panel—and to view its properties—right-click. You can add items to your GNOME menus.

To add to the main menu, create a .desktop file in the /usr/share/applications directory. The easiest way is to copy an existing .desktop file that is in the menu you want and modify it. For example, to add a video player to the Sound & Video menu, you can do the following (as root user):

```
# cd /usr/share/applications
# cp gnome-cd.desktop vidplay.desktop
```

Next, use any text editor to change the contents of the vidplay.desktop file you created by adding a comment, a file to execute, an icon to display, and application name. After you save the changes, the new item immediately appears on the menu (no need to restart anything).
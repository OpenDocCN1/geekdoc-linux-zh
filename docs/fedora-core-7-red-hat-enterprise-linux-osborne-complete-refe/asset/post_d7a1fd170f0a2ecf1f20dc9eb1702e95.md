
launcher for one that is not. Launchers can be added to a panel by just dragging them directly. Launchers include applications, windows, and files.

### Application Launchers

If an application already has an application launcher, to add it to a panel is easy. You just have to drag the application launcher to the panel. This will automatically create a copy of the launcher for use on that panel. Launchers can be menu items or desktop icons. All the entries in your *Application* menu are application launchers. To add an application from the menu, just select it and drag it to the panel. You can also drag any desktop application icon to a panel to add a copy of it to that panel.

For any menu item, you can also go to its entry and right-click it. Then select the **Add This Launcher To Panel** entry. An application launcher for that application is then automatically added to the panel. Suppose you use Gedit frequently and want to add its icon to the panel, instead of having to go through the *Application* menu all the time. Right-click the *Text Editor* menu entry in the *Accessories* menu, and select the **Add This Launcher To Panel** option. The Gedit icon now appears in your panel.

You can also select the **Add To Panel** entry from the panel menu and then choose the *Application Launcher* entry. This will display a box with a listing of all the *Application* menu entries along with *Preferences* and *Administration* menus, expandable to their items. Just find the application you want added and select it. This may be an easier approach if you are working with many different panels.

Keep in mind that for any launcher that you previously created on the desktop, you can just drag it to the panel to have a copy of the launcher placed on the panel.

### Folder and File Launchers

To add a folder to a panel, just drag it directly from the file manager window or from the desktop. To add a file, also drag it directly to the panel, but you will then have to create a launcher for it. The *Create Launcher* window will be displayed, and you can give the file launcher a name and select an icon for it.

### Adding Drawers

You can also group applications under a *Drawer* icon. Clicking the *Drawer* icon displays a list of the different application icons you can then select. To add a drawer to your panel, right-click the panel and select the **Add To Panel** entry to display the **Add To** list. From that list select the *Drawer* entry. This will create a drawer on your panel. You can then drag any items from desktop, menus, or windows to the *drawer* icon on the panel to have them listed in the *drawer*.

If you want to add, as a *drawer*, a whole menu of applications on the main menu to your panel, right-click any item in that menu, and then select **Entire Menu** from the pop-up menu, and then select the **Add This As Drawer To Panel** entry. The entire menu appears as a *drawer* on your panel, holding icons instead of *menu* entries. For example, suppose you want to place the *Internet Applications* menu on your panel. Right-click any entry item, selecting **Entire Menu**, and select **Add This As Drawer To Panel**. A *drawer* appears on your panel labeled *Internet*, and clicking it displays a pop-up list of icons for all the *Internet* applications.

### Adding Menus

A menu differs from a drawer in that a *drawer* holds application icons instead of menu entries. You can add menus to your panel, much as you add drawers. To add a submenu from the Applications menu to your panel, right-click any item and select **Entire Menu**, and then select the **Add This As Menu To Panel** entry. The menu title appears in the panel; you can click it to display the menu entries.

You can also add a menu from the panel’s **Add To** list, by selecting **Custom** menu.

### Adding Folders

You can also add directory folders to a panel. Click and drag the **Folder** icon from the file manager window to your panel. Whenever you click this **Folder** button, a file manager window opens, displaying that directory. You already have a **Folder** button for your home directory. You can add directory folders to any drawer on your panel.

### Special Panel Objects

Special panel objects perform operations not supported by other panel objects. Currently, these include the **Lock**, **Logout**, and **Launcher** buttons, as well as the *status dock*. The **Lock** button, which displays a padlock, will lock your desktop, running the screensaver in its place. To access your desktop, click it and then enter your user password at the password prompt. The **Logout** button shows an open door. Clicking it will display the **Logout** dialog box, and you can then log out. It is the same as selecting **Logout** from the desktop menu. The **Launcher** button shows a launcher icon. It opens the **Create Launcher** dialog box, which allows you to enter or select an application to run.

The *status dock* is designed to hold status docklets. A status docklet provides current status information on an application. KDE applications that support status docklets can use the GNOME status dock, when run under GNOME.

## GNOME Applets

*Applets* are small programs that perform tasks within the panel. To add an applet, right-click the panel and select **Add To Panel** from the pop-up menu. This displays the **Add To** box, listing common applets along with other types of objects, such as launchers. Select the one you want. For example, to add the **Clock** to your panel, select **Clock** from the panel’s **Add To** box. Once added, the applet will show up in the panel. If you want to remove an applet, right-click it and select the **Remove From Panel** entry.

GNOME features a number of helpful applets. Some applets monitor your system, such as the **Battery Charge Monitor**, which checks the battery in laptops, and **System Monitor**, which shows a graph indicating your current CPU and memory use. The **Volume Control** applet displays a small scroll bar for adjusting sound levels. The **Deskbar** tool searches for files on your desktop. **Network Monitor** lets you monitor a network connection.

Several helpful utility applets provide additional functionality to your desktop. The **Clock** applet can display time in a 12- or 24-hour format. Right-click the **Clock** applet and select the **Preferences** entry to change its setup. The **CPU Frequency Scaling Monitor** displays CPU usage for CPUs like AMD and the new Intel processors that run at lower speeds when idle.

### Workspace Switcher

The *Workspace Switcher* appears in the panel and shows a view of your virtual desktops (see Figure 6-8). Virtual desktops are defined in the window manager. Located on the right side of the lower panel, the Workspace Switcher lets you easily move from one desktop to another with the click of a mouse. It is a panel applet that works only in the panel. You can add the Workspace Switcher to any panel by selecting that panel's Add To box.

The Workspace Switcher shows your entire virtual desktop as separate rectangles listed next to each other. Open windows show up as small colored rectangles in these squares. You can move any window from one virtual desktop to another by clicking and dragging its image in the Workspace Switcher. To configure the Workspace Switcher, right-click it and select Preferences to display the Preferences dialog box. Here, you can select the number of workspaces. The default is four.

### GNOME Window List

The *Window List* shows currently opened windows (see Figure 6-8). The Window List arranges opened windows in a series of buttons, one for each window. A window can include applications such as a Web browser or be a file manager window displaying a directory. You can move from one window to another by clicking its button. When you minimize a window, you can later restore it by clicking its entry in the Window List.

Right-clicking a window's Window List button opens a menu that lets you Minimize or Unminimize, Roll Up, Move, Resize, Maximize or Unmaximize, or Close the window. The Minimize operation will reduce the window to its Window List entry. Right-clicking the entry will display the menu with an Unminimize option instead of a Minimize one, which you can then use to redisplay the window. The Roll Up entry will reduce the window to its title bar. The Close entry will close the window, ending its application.

If there is not enough space on the Window List applet to display a separate button for each window, then common windows will be grouped under a button that will expand like a menu, listing each window in that group. For example, all open terminal windows would be grouped under a single button, which when clicked would pop up a list of their buttons.

The Window List applet is represented by a small serrated bar at the beginning of the window button list. To configure the Window List, right-click this bar and select the Properties entry. Here, you can set features such as the size in pixels, whether to group windows, whether to show all open windows or those from just the current workspace, or which workspace to restore windows to.

### GNOME Configuration

You can configure different parts of your GNOME interface using tools listed in the Preferences menu in the System menu. This menu will display entries for the primary GNOME preferences organized into submenu categories like Hardware and Personal, along with preferences listing task-specific tools, like that for the Palm Pilot or Desktop Switcher. Selecting one will open a window labeled with the tool name, like mouse preferences.

Your GNOME system provides several desktop tools you can use to configure your desktop, such as *Desktop Background*, *Screensaver*, and *Themes*. You use the Desktop Background applet to select a background color or image, the Screensaver to select the screen saver images and wait time, and the Theme tool to choose a theme (see Figure 6-9).

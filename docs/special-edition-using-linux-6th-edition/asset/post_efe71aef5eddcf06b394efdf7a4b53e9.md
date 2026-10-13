
The K Menu selections configure the Application Starter. The Merge Different Menu Locations option determines whether the personal and system menus are merged into one, or listed separately. The Show Recent Documents Submenu determines whether Recent Documents entry is available. Similarly, the Show Quickbrowser Submenu determines whether the Quick Browser is available on the Application Starter.

## BUTTONS

The Buttons tab configures the appearance of individual buttons on the panel. If you turn on background tiles, then each type of tile can be colored differently. For each type of tile, select whether it should be specially colored by clicking the Enabled check box. Then select the color from the drop-down list.

## APPLETS

The Applets tab determines what applets are available for embedding in the panel and how they run. Applets are applications such as the taskbar, pager, and dock.

Applets can either run internally or externally. To the end user, there is little difference, except that internal applets run faster. The problem with internal applets is that if they are unstable or insecure, the entire panel can crash or be compromised. The panel is protected from external applets by a wrapper script. That way, if the applet crashes, the panel is unaffected.

You can choose one of the following security levels:

- **Load only trusted applets internal**—Applets listed in the Trusted Applets list will be loaded internally. All other applets will be loaded externally. You can move applets between the Trusted and Available lists using the arrow buttons between the two lists.
- **Load startup config applets internal**—Applets that are configured to run on startup are loaded internally. Applets started later are loaded externally. This is usually a good selection.
- **Load all applets internal**—Trusts all applets. This will improve performance, but can decrease stability.

## ADJUSTING ITEMS ON THE PANEL

To move an item on the Panel, or to remove an item from the Panel, use the options on the context menu for that item. Right-click an item and the context menu appears (see Figure 3.9). To move an item, select the Move option on this menu, and drag the item to the desired position on the Panel. Other buttons on the panel shift to make room for the item when you drop it. You can also move an item by clicking it and dragging with the middle mouse button. To remove an item, select Remove from the context menu.

## ADDING ITEMS TO THE PANEL

Adding items to the panel is fairly simple. Just select Panel Menu, Add from the Application Starter. This will provide several classes of items to add:

![](img/c741b1b6b6eccaba2ad43454c979a7f8_72_0.png)

- **Application**—This provides a list of all the applications on the Application Starter. Selecting one will add a short-cut button to that application.
- **Applet**—This provides a list of known applets. Applets include the taskbar, the pager, the clock, and the dock. Things in the dock such as klipper are not applets. The list of available applets is determined by the desktop files in `${KDEDIR}/share/apps/kicker/applets`.
- **K Menu**—This adds an Application Starter. You can have multiple Application Starters if you like. For example, you might put one on each side of the panel for easier access. You can also remove the Application Starter altogether if you would rather have the panel space. As with most things in KDE, everything on the Application Starter is available through other means.
- **Windowlist**—This adds a button that provides quick access to all applications running on all desktops.
- **Desktop Access**—This adds a button that, when pressed, temporarily hides all the windows on the desktop. This makes it easy to get to icons on your desktop (such as the Trash). Pressing this button again restores all your windows.
- **Quick Browser**—This adds a Quick Browser, after asking you for the directory you would like to view. Quick Browsers give easy access to directories by making all of the directory entries appear as menu entries.
- **Legacy Application**—This adds a non-KDE application shortcut. KDE applications will automatically add themselves to the Application Starter, so you can just select them from the Application list, but non-KDE applications don’t do this. Selecting Legacy Application allows you to add these applications easily.

**Figure 3.9**
The Panel item context menu pops up when you right-click an item on the Panel.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_73_0.png)

## Using the Menu Editor

The menu editor, kmenuedit, modifies the main Application Starter menu. To open the menu editor, select System, Menu Editor on the Application Starter menu. Figure 3.10 shows the menu editor window.

To open or close submenus, click the box beside a name. To move a menu item from one location to another, drag it using the mouse.

To create a new menu item, select the submenu you want to add it to and select File, New Item (or click the New item button on the toolbar). On the General tab, the fields are as follows:

- **Name**—Language-specific name of application. This is the name that appears in the menu.
- **Comment**—Longer comment for application. This appears in the quick-tip for the application.
- **Command**—Command to run.
- **Type**—Generally this should be Application.
- **Work Path**—Directory to change to before running application.
- **Run in terminal**—If selected, application will be run in a terminal. The terminal will be started with the options listed in the Terminal Options textbox.
- **Run as different user**—If selected, application will be run as user specified in the Username textbox. You will have to enter the password for that user whenever you execute this command.
- **Icon**—The button beside Work Path allows you to select an icon for this application.

**Figure 3.10**  
The Menu Editor for the Application Starter menu.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_74_0.png)

> **Tip**
> Unlike older versions of KDE, you no longer have to worry very much about whether a particular desktop file is in the system directory or in your personal directory. If you try to edit a system entry, kmenuedit will automatically make a copy to your local directory. The two locations are merged in the Application Starter menu, so it all works transparently.

## Restart Option

After making adjustments to the Panel or Application Starter menu contents, it might be necessary to restart the Panel program in order for the changes to take effect. To restart the Panel, select Panel Menu, Restart on the Starter menu, or choose Restart from the Panel context menu. Few changes, however, require restarting the panel.

## Manipulating Files and Directories

The file manager, konqueror, is such an integral part of KDE that it deserves special discussion. This section covers how to use konqueror to manipulate files and directories, as well as to navigate remote filesystems and view World Wide Web pages.

### Introduction to the File Manager

konqueror is different from other file managers that you might have encountered because it treats all the objects that it browses in a very consistent manner. konqueror is really a generic browser, capable of viewing not only file and directory listings, but many other things as well. The way konqueror achieves this is by using Uniform Resource Locators (URLs) for all the paths that it browses and by using plug-in modules to display various types of information. Thus, in addition to being a filesystem browser and manager, konqueror is also an FTP client, a World Wide Web browser, an archive file viewer, an image viewer, and much more.

### Location Transparency

Because all the separate things that konqueror can browse are treated the same, it enables you to perform operations conveniently, with little regard for the location of the item you are manipulating. For example, you can drag links from a World Wide Web page onto your Desktop, where you can click them at any time to call them up. You can do the same thing for FTP directories, placing them on your Desktop just like folders. When you click a file on a remote FTP site, konqueror launches it or opens it as if it were a local file. The only difference is that it might take longer as konqueror downloads the file to your system to operate on it.

In another example, you can drag files directly from a remote FTP site (in a folder in konqueror) directly to another KDE application running on your Desktop. You can drag a package file on an FTP site directly to the package manager program to view the package information and install it on your system.

This kind of seamless interaction between remote and local objects makes it easier to access and manage the things you work with on a day-to-day basis.

> **Tip**
>
> Not all KDE applications are as location transparent as konqueror. Just because you can click an FTP site’s text file and automatically pull up a text editor doesn’t mean that saving from the editor will automatically upload the file back to the FTP site. Unfortunately, you might find that when you file away the file, you are simply touching the temporary file, which will be deleted when you close the text editor. Hopefully this will be improved in future versions of KDE.

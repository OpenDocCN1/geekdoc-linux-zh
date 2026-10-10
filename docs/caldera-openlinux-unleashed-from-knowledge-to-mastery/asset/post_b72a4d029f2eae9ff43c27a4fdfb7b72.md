
![](img/df365d352a104b50fea29e59a052de4d_156_0.png)

Clicking the Add Application entry opens a cascaded menu of all available KDE applications. When you select an application, its icon is added directly to the panel. You can then launch the application by clicking the icon in the panel. This is a great time-saver for frequently used applications.

The Add Disk Navigator and Add Windowlist entries add special buttons to the panel. The disk navigator button lets you access the disk navigator directly from the panel without going through the K menu. The window list button adds to the panel a special button that lists all windows on the desktop. Selecting a window opens it (if it is minimized) and brings it in front of other windows.

The Configure entry lets you configure the panel. You can control its location (top, bottom, left or right) and size. You can also control the location of the taskbar (recall that the taskbar is a small bar that holds a button for each active window).

From the Configure entry, you can also set the number of virtual desktops and other aspects of the panel's behavior. For more details, consult the KDE help entry for the panel application.

The Edit Menus entry lets you edit the K menu. Selecting it starts a special menu-editing application as well as the help screen for the menu editor. The menu editor is fairly easy to use, and the help documentation is reasonable. However, one thing that may not be obvious is that the K menu is divided into a system-wide standard part and a per-user part. You can edit your per-user part, but only root can edit the system-wide menu.

The Restart entry restarts the panel. Although you can customize the panel using KDE applications, you can also customize it by editing text files. Section 4 of the KDE Help entry The K Panel Handbook describes how to edit the files. Selecting Restart causes the panel to reread its configuration from the text files.

On the panel, you can reconfigure any button by dragging it while holding mouse button 2. If you click button 3 over an icon, a pop-up menu will appear. This menu will let you move or remove an icon, or edit its properties. The properties you can edit are

- **General properties** The file name of the icon.
- **Permissions** UNIX permissions of the target of the icon.
- **Execute** Program to execute and how to run it. You can also select a new image for the icon by clicking the *icon* button on the *Execute* tab.
- **Application** The human-readable page name of the application that the button will launch. Whatever you place in the *Comment* field in this panel appears as pop-up help balloons when the mouse pointer hesitates over the button.

The panel can swallow X Window programs. This means that the programs appear right in the panel rather than in their own window. For details of how to do this, see Section 3 of the KDE Panel help page.

## Virtual Desktops

Near the center of the panel are buttons for switching virtual desktops. KDE divides your workspace into as many as eight (four by default) virtual desktops. Think of these as extra work areas that can hold additional windows. By clicking the virtual desktop buttons on the panel, you can switch to a different desktop. You can arrange your work so that, for example, your Web browser is on one desktop, your email client is on another desktop, and your text editor is on a third. This lets you make efficient use of screen space.

One nice touch is the integration of the virtual desktop scheme with the taskbar. If you press a button on the taskbar that belongs to a window in a different virtual desktop, KDE automatically changes to the desktop containing the window. This makes it even more convenient to arrange your work in multiple virtual desktops.

## The Desktop Menu

Pressing button 3 over the desktop background brings up the desktop menu (Figure 5.6).

The desktop menu entries are described in Table 5.1.

**FIGURE 5.6**

*Desktop menu.*

![](img/df365d352a104b50fea29e59a052de4d_157_0.png)

### TABLE 5.1 Desktop Menu Entries

| Entry | Meaning |
| :--- | :--- |
| New | Brings up a submenu that allows you to create new files, folders, URLs, application icons, and so forth. |
| Bookmarks | Brings up a submenu that displays any bookmarks you have created with the file manager. The menu also has an entry for editing existing bookmarks. |
| Help on desktop | Brings up the KDE help browser. |
| Execute command | Prompts you to type a command and then executes it. You can press Alt+F2 as a shortcut. This entry is useful for typing commands if you don't have a shell window open. |
| Display properties | Brings up the KDE display property editor, which allows you to change the background, colors, fonts, style, and screen saver. |
| Refresh desktop | Causes all windows to redisplay their contents (in case a buggy program disturbed the display). |
| Unclutter windows | Moves windows so that the maximum amount of each window is visible. |
| Cascade windows | Moves windows so that they occupy as little of the desktop as possible. |
| Arrange icons | Arranges desktop icons neatly. |
| Lock screen | Locks the screen with a password-protected screen saver. |
| Log out | Terminates the KDE session. |

## The KDE File Manager

The KDE file manager, `kfm`, is a file manager and Web browser in one. You can use it to navigate your file system and browse the Web. The file manager is also responsible for the desktop icons, which provide convenient shortcuts to commonly used files and applications.

To start the file manager, click the home directory icon on the panel. (See Figure 5.3.)
The KDE file manager starts. (See Figure 5.7.)

To open a file or folder, click it once with button 1.

> **Note**
>
> Most KDE programs require only a single click to perform an action. Unlike most GUIs (including Microsoft Windows), KDE programs require a double-click to open a file or launch an application. Single-click activation is the way most Web browsers work, but it takes some getting used to in a file manager.

![](img/df365d352a104b50fea29e59a052de4d_158_0.png)

# FIGURE 5.7
KDE file manager.

![](img/df365d352a104b50fea29e59a052de4d_159_0.png)

Use the file manager’s toolbar to perform the following operations:

- To change to the parent directory of the current directory, click **Up**.
- To go back to the last directory (retrace your steps), click **Back**.
- To undo the last Back step, click **Next**.
- To change to your home directory, click **Home**.
- To refresh the current display, click **Refresh**.

Click the question mark button to bring up the KDE file manager’s help page. This page explains additional features of the file manager.

## Selecting Files

Normally, clicking a file opens it. If you just want to select a file to perform some operation on it (like deleting it), you have a couple of options:

- To select a single file and perform an operation on it, click the file with button 3. A menu will pop up. From this menu, you can delete the file, move it to the trash, or edit its properties. Within the property editor, you can change the file’s name, permissions, and icon.
- To select several files, hold the Control key down and click button 1 on each file. If you wish to deselect a selected file, hold down Control and click again. After you have selected the files, you can open a menu with button 3 and operate on all the files.

## Views

The View menu lets you alter the appearance of files in the file manager. The normal view is called Icon View and displays files and directories as little icons. The other kinds of views are:

- Text View A display similar to the output of the `ls -l` command.
- Long View Similar to Text View, but with small icons on the left-hand side of the listing.
- Short View A display similar to the output of the `ls` command, but with small icons to the left of each file name.

In addition, the Show Tree option turns on a tree-like display of the directory structure starting from the file system root, your home directory, and your Desktop directory.

## The Desktop Directory

Any files deposited in the Desktop directory under your home directory appear as icons on the desktop surface itself. You can create these icons in a number of ways:

- Using the KDE file manager, simply create a directory or file in Desktop. It will appear as an icon.
- Drag a file or directory from the KDE file manager onto the desktop background. A small menu with the Copy, Move, and Link options will appear. The Copy operation will copy the file or directory from its source location into the Desktop directory. The Move operation will move the file or directory into the Desktop directory (and remove it from its original location). Finally, the Link operation will place a symbolic link to the file in Desktop. This will appear as an icon with a little arrow, denoting a shortcut.

## URLs

Not only is the KDE file manager a handy tool for navigating your file system, but it is also a full Web browser. In the Location text entry box, just type a URL like http://www.roaringpenguin.com to open a Web page. You can also open FTP URLs and use the file manager as an FTP client.

Anything you can view with the file manager can be made into a desktop icon. You can even drag links from a Web page and drop them on the desktop. This will create an icon that, when clicked, will take you instantly to the URL.

## Bookmarks

The KDE file manager Bookmarks menu allows you to add the current location to your set of bookmarks. Bookmarks are links to often-visited files and URLs. They let you organize your browsing and work exactly as bookmarks in Web browsers do. Any bookmarks you create with the file manager are available from the button 3 pop-up menu on the desktop background.

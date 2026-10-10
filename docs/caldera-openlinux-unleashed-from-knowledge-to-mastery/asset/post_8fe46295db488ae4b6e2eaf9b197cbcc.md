
To permanently close a window, click the close button. If the window is the main window of an application, the application will terminate. If it is just one of several open application dialog boxes, usually just the window will disappear. However, various applications may respond in different ways to the close button—you need to experiment.

The menu button provides a pull-down menu of window operations. To see the menu, click the menu button. Applications can add extra entries to the window menu; however, all applications have the following entries:

- ***Maximize*** Corresponds to the maximize button. If a window is already maximized, the menu entry reads *Restore*.
- ***Iconify*** Corresponds to the minimize button.
- ***Move*** Allows you to move the window by moving the mouse pointer. Click button 1 when the window is where you want it.
- ***Resize*** Allows you to resize the window. As you move the mouse pointer, an outline of the window shows its new size. When it is the size you want, click button 1 to make the size change take effect.
- ***Sticky*** Makes a window “sticky”. KDE supports virtual desktops. Imagine that the actual KDE desktop is much larger than your monitor is. A virtual desktop is a monitor-sized window inserted into this larger desktop. KDE allows you to switch between virtual desktops by clicking buttons on the panel. A sticky window “sticks” to the monitor and is always visible, even if you change virtual desktops. Normal windows disappear when you switch away from their virtual desktop. (All this is discussed in more detail in the section entitled “The Panel” later in this chapter.)

The little push-pin button next to the menu button toggles a window between sticky and normal. When a window is sticky, the pin changes position so the window looks pinned to the screen.

- ***To Desktop...*** Allows you to move a window to a different virtual desktop. You select which desktop you want from a submenu.
- ***Close*** Corresponds to the close button.

## Window Title Bars

If you have many windows on the screen, they will probably overlap. To raise a window, click mouse button 1 in the window’s title bar. The window will move in front of all other windows. You can also achieve this by holding down the Alt key and clicking button 2 anywhere in the window.

To lower a window, click button 2 in the window’s title bar. The window will move behind all other windows. In addition, pressing Alt+button 2 anywhere in the window moves the window behind other windows if it is currently in front of all other windows.

To shade a window, double-click button 1 in the window's title bar. The window disappears, leaving only the title bar. Double-click once more in the title bar to restore the window.

To move a window, drag the window's title bar. The window follows the mouse pointer as you drag it. You can also move a window by holding down Alt and dragging anywhere in the window with button 1.

> **Note**
>
> These mouse clicks are the defaults for KDE. You can configure KDE to react to mouse clicks any way you prefer. The section entitled "KDE Control Center" describes how to configure KDE.

## Resizing a Window

To resize a window, move the mouse pointer to the very edge or corner of the window frame. This can be quite tricky and takes a bit of practice. After the pointer is in the right place, it changes to a bar with an arrow. The direction of the arrow shows the direction in which the window will be resized. For example, if you move near the top left-hand corner of the window frame, the mouse pointer changes to a resize pointer that looks like this: ⇖

With the resize cursor, drag the corner or edge of the window to resize it. An outline illustrates how the final window will look. After you have resized the window to the desired size, release the mouse button and the window will resize.

You can also resize a window by holding down the Alt key and dragging anywhere in the window with button 3.

## The Panel

The panel is a bar that appears on one side of the screen. It provides a convenient central place for launching applications. A typical panel is shown in Figure 5.3.

![](img/df365d352a104b50fea29e59a052de4d_153_0.png)

## Hiding the Panel

The two textured bars on each end of the panel contain little arrows. Click either of the two bars to shrink the panel. The panel shrinks down to a tiny bar on one side of the screen. Click on the tiny bar to make the panel reappear.

Note that when you shrink the panel, the K button, a window list button, and a disk navigator button appear in a tiny box in the top left-hand corner of the screen. These select buttons give you access to the most common panel functions without having to re-expand the entire panel bar.

## The Application Starter

The official title of the K button is the Application Starter, but we will refer to it simply as the K button. Clicking it brings up the KDE application menu shown in Figure 5.4.

![](img/df365d352a104b50fea29e59a052de4d_154_0.png)

With the KDE application menu, you can launch most KDE applications without typing a command line. The first group of entries on the menu is a list of categories (Development, Documentation, Editors, Games, Graphics, Internet, Multimedia, Office, Toys, and Utilities). Clicking these entries brings up a submenu of application programs. The organization of programs into general categories makes the menu tidier and helps you navigate the contents of your disk.

The second group of entries (*Settings*, *System*, and *COAS*) brings up programs related to desktop configuration and system administration. *Settings* lets you customize KDE itself, changing its appearance and behavior to suit your taste. *System* provides access to various system configuration and information tools. Feel free to experiment with some of these tools; they are too numerous to be covered in this chapter. *COAS* provides access to the Caldera Open Administration System, a graphical configuration system for Linux. The administration tools are covered in Chapter 10.

The next group of entries (*Word Processing*, *Applications*, *KDE Help*, *Home Directory*, and *KDE Control Center*) includes other applications that (for some unknown reason) are not categorized in the first group. The most important menu entry in this group is *KDE Help*, which launches the KDE help browser. The KDE help browser includes help for most KDE programs, as well as being a one-stop browser for system man and information pages. The separation of documentation into traditional manual pages, GNU-style information pages, and KDE HTML pages is unfortunate. The KDE help browser mitigates this by providing access to all these resources from one application. Use KDE Help. You’ll like it.

The *Home Directory* entry opens a file manager at your home directory. The file manager will be described later in this chapter in the section entitled “The KDE File Manager.”

*KDE Control Center* starts an application that lets you customize the look and feel of KDE. It is described in the next section, “The KDE Control Center.”

The *Personal menu* brings up a menu of personal and non-KDE applications. You can customize this menu; it is described in more detail in the section entitled “Customizing the Panel” later in this chapter.

The *Disk Navigator* menu presents the entire *Linux* file system as a series of cascading menus. You can walk through your home directory, your CD-ROM, or the root directory simply by passing from menu to menu. The disk navigator also remembers recent files and applications you have used and presents them in a *Recent* section.

*Lock Screen* and *Logout* do exactly what they say they do. The screen locker is password-protected with your UNIX password. The *Logout* entry terminates your KDE session. However, the *KDE window manager* saves the state of your desktop so that the next time you start KDE, the same applications are opened at the same locations as when you logged out.

## Customizing the Panel

From the *K* menu, select *Panel* to customize the panel. The panel customization menu (Figure 5.5) pops up.

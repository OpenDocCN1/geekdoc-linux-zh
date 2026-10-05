
# KDE 283

When you move windows, they 'magically' snap to the borders of the desktop as well as to the borders of other windows. The extent of the span zones can be modified in the DESKTOP|DESKTOP dialog. (O switches the snap function off.)

# Window title animation

If the window is too narrow to display the window title, the window title moves the title line like in a newsflash. This more irritating than useful animation can be switched off in WINDOWS|TITLEBAR.

# Screen saver

KDE contains a whole palette of screen savers. The configuration is carried out in DESKTOP|SCREENAVER.

Further configuration options will be described in the following sections.

# The KDE panel

The panel (KPanel for short) is the central control component of KDE. It assists starting with programs, switching between running programs, switching between desktops, and so on. In the default configuration, KPanel is displayed at the bottom of the screen; buttons with a list of all running programs (comparable to the Windows taskbar) are at the top of the screen (see Figure 8.5).

The two most important icons of KPanel are the three-dimensional letter K, which leads to the KDE start menu, and the window icon which permits easy switch between running programs. (The contents of this menu are also displayed via [Ctrl|Esc] or after clicking the mouse button on the desktop.)

The remaining preconfigured icons are used for starting various KDE programs (file manager, help system, and so on) and save the laborious navigation through the levels of the start menu. Finally, the letter X for shutdown of KDE and the padlock icon for temporary locking of the screen are important. (Work in KDE can only be continued after entering the login password. Until then, a screen saver is activated.

# Panel configuration

Options for the look of the panel can be set via the context menu as well as via APPLICATIONS|PANEL in the KDE control center. There, together with other items, the panel and taskbar positions can be determined (top, bottom, or left). The taskbar can also be made visible. (To switch between running programs, the WINDOWLIST panel or various mouse or keyboard shortcuts can be used.)

Now to the contents of the panel: the displayed icons can be moved with the mouse button. With the right mouse button, you can call a context menu. The commands can also alter the properties of the entry. The form can be modified on the dialog sheet EXECUTE by clicking on the square icon buttons. This triggers the display of an almost endless list of premanufactured KDE icons. (As long as no icon is set, the icon button is displayed as an empty, gray surface.)

# 284 X USER INTERFACES (FVWM, KDE, and GNOME)

![](img/b30873dd3d753687a59253fb9ad26a0b_311_0.png)

Figure 8.7 Properties of a panel icon.

The icon list displayed on the panel is extended via the KDE start menu, entry PANEL ADD APPLICATION. The menu contains a list of all programs appearing in the start menu.

This immediately raises the question of how the start menu can be modified: you need to execute PANEL EDIT MENUS. The menu editor that appears now (kmenuedit) shows the current start menu as well as the individual menu (which is simply a submenu of the start menu). You can now open individual submenus by clicking on them (and by repeated clicking them again). Via a context menu, you can change existing entries: with drag & drop you can copy individual entries; and with the middle mouse button you can change the order of the entries.

![](img/b30873dd3d753687a59253fb9ad26a0b_311_1.png)

Figure 8.8 The KDE menu editor.

# Executing programs in an icon

Usually, programs are displayed in a separate window at start-up. However, in a few cases it makes sense for the output of the program to appear directly in an icon on the panel. To configure an icon in such a way, you have to fill in both panel text fields. The window title is crucial: this is where you specify that the program displays in the window title (when it is started normally). KPanel requires the text to catch the window (so to speak).

![](img/b30873dd3d753687a59253fb9ad26a0b_312_0.png)

Figure 8.9 Properties of a panel icon.

# Panel tools

Panel tools are small programs which display status at KPanel. Important examples are kbiff (displays whether mail has been received), kpneum (displays CPU load), and kapm (displays battery).

If you want panel tools to be started automatically, you must create a link to the desktop. To do this, simply drag the program from the file manager onto the desktop.

# Virtual desktops

In the default configuration, KDE manages desktops, between which you can switch. The number of desktops can be modified in the control center under PANEL|DESKTOPS.

# Desktop pager

A-called desktop pager (pager) can assist with the management of desktops. This is a program which offers a reduced view of all desktops.

![](img/b30873dd3d753687a59253fb9ad26a0b_313_0.png)

Figure 8.10 The KDE pager.

# Icons on the desktop

In the default configuration, KDE displays three icons on the desktop. These are symbols for the directories. With drag & drop via the context menu NEW, you can put any number of additional icons on the desktop.

# 287 KDE

Let us assume that you wish to create an icon for the CD-ROM. To do this, you activate the desktop context menu NEW|DEVICE.

![](img/b30873dd3d753687a59253fb9ad26a0b_314_0.png)

Figure 8.11 CD ROM icon.

If you now click on the icon, the CD-ROM is mounted into the directory tree at the point /edrom. Simultaneously, the KDE manager is started and displays the contents of the CD-ROM. To unmount the CD-ROM from the directory tree (umount), simply click the icon with the right mouse button and execute UNMO.

# Disk Navigator

Besides numerous bug fixes and improvements of details, the Disk Navigator is the only true novelty of KDE 1.1 against 1.0. It is a script extension to the KDE start menu, which helps you to quickly open a window for a specific directory with the file manager or a shell terminal.

To start the file manager in a specific directory, simply use the menu entries of the Disk Navigator. For each subdirectory, a separate submenu is provided. When you select the OPEN FOLDER entry together with Shift a terminal window is opened in which the selected directory is set as the current directory.

Under the RECENT menu entry, the four most recently selected files, directories, or programs started via the KDE menu are displayed.

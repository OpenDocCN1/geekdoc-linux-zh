# GNOME DESKTOP TERMINOLOGY

The following terminology, which is taken from the GNOME Users Guide, establishes a foundation for discussing the GNOME desktop. Figure 4-2 on page 92 shows the initial Fedora GNOME desktop.

Desktop The *desktop* comprises all aspects of the GNOME GUI. While you are working with GNOME, you are working on the desktop. There is always exactly one desktop.

Panels Panels are bars that appear on the desktop and hold (panel) objects. Initially there are two gray panels: one along the top of the screen (the Top Edge panel, or just Top panel) and one along the bottom (the Bottom Edge panel, or just Bottom panel). You can add and remove panels. You can place panels at the top, bottom, and both sides of the desktop, and you can stack more than one panel at any of these locations. The desktop can have no panels, one panel, or several panels. See page 111 for more information on panels.

Panel objects Panel objects appear as words or icons on panels. You can click these objects to display menus, run applets, or launch programs. The five types of panel objects are applets, launchers, buttons, menus, and drawers. See page 113 for more information on panel objects.

Windows A graphical application typically runs within and displays a window. At the top of most windows is a titlebar you can use to move, resize, and close the window. The *root window* is the unoccupied area of the workspace and is frequently obscured. The desktop can have no windows, one window, or many windows. Although most windows have decorations (page 142), some, such as the Logout window, do not.

Workspaces Workspaces divide the desktop into one or more areas, with one such area filling the screen at any given time. Initially there are two workspaces. Because panels and objects on the desktop are features of the desktop, all workspaces display the same panels and objects. By default, a window appears in a single workspace. The Switcher (page 95) enables you to display any one of several workspaces.

Tooltips Tooltips (Figure 4-2, page 92) is a minicontext help system that you activate by moving the mouse pointer over a button, icon, window border, or applet (such as those on a panel) and allowing it to hover there. When the mouse pointer hovers over an object, GNOME displays a brief explanation of the object.

# OPENING FILES

By default, you double-click an object to open it; alternatively, you can right-click the object and select **Open** from the drop-down menu. When you open a file, GNOME figures out the appropriate tool to use by determining the file's *MIME* (page 1094) type. GNOME associates each filename extension with a MIME type and each MIME type with a program. Initially GNOME uses the filename extension to try to determine a file's MIME type. If it does not recognize the filename extension, it examines the file's *magic number* (page 1092).

For example, when you open a file with a filename extension of ps, GNOME calls the Evince document viewer, which displays the PostScript file in a readable format.

## GTK+

GTK+ is the widget set used for GNOME applications. Its look and feel was originally derived from Motif. The widget set is designed from the ground up for power and flexibility. For example, buttons can have labels, images, or any combination thereof. Objects can be dynamically queried and modified at runtime. It also includes a theme engine that enables users to change the look and feel of applications using these widgets. At the same time, the GTK+ widget set remains small and efficient.

The GTK+ widget set is entirely free under the Lesser General Public License (LGPL). The LGPL enables developers to use the widget set with proprietary software, as well as free software (the GPL would restrict it to just free software). The widget set also features an extensive set of programming language bindings, including C++, Perl, Python, Pascal, Objective C, Guile, and Ada. Internationalization is fully supported, permitting GTK+-based applications to be used with other character sets, such as those in Asian languages. The drag-and-drop functionality supports both Xdnd and Motif protocols, allowing drag-and-drop operations with other widget sets that support these protocols, such as Qt and Motif.

## The GNOME Interface

The GNOME interface consists of the panel and a desktop, as shown in Figure 6-1. The panel appears as a long bar across the bottom of the screen. It holds menus, programs, and applets. (An applet is a small program designed to be run within the panel.) On the panel is a button with a large red hat on it. This is the GNOME applications menu, the main menu. The menu operates like the Start menu in Windows, listing entries for applications you can run on your desktop. You can display panels horizontally or vertically, and have them automatically hide to show you a full screen.

The remainder of the screen is the desktop. Here, you can place directories, files, or programs. You can create them on the desktop directly or drag them from a file manager window. A click-and-drag operation will move a file from one window to another or to the desktop. A click and drag with the CTRL key held down will copy a file. A click-and-drag operation with the middle mouse button (two buttons at once on a two-button mouse) enables you to create links on the desktop to installed programs. Initially, the desktop holds only an icon for your home directory. Clicking it opens a file manager window to that directory. A right-click anywhere on the desktop displays a desktop menu (see Table 6-1) with which you can open new windows, create new folders, and mount floppy disks and CD-ROMs.

> Tip You can display your GNOME desktop using different themes that change the appearance of desktop objects such as windows, buttons, and scroll bars. GNOME functionality is not affected in any way. You can choose from a variety of themes. Many are posted on the Internet at themes.freshmeat.net. Technically referred to as GTK themes, these allow the GTK widget set to change their look and feel. To select a theme, use the GNOME Control Center and select Themes in the Desktop listing.

![](img/6c226e8ba1efd427dec3bf582418d33f_131_0.png)

FIGURE 6-1 GNOME

## GNOME Components

From a user's point of view, you can think of the GNOME interface as having four components: the desktop, the panel, the main menu, and the file manager. In its standard default configuration, the GNOME desktop displays a Folder icon for your home directory in the upper-left corner, along with a trash can to delete items, and a Start Here icon for accessing applications and setting preferences. Some distributions may include other icons, such as links to the GNOME Web site or to the Linux documentation site. Initially, a file manager window opens on the desktop, displaying your home directory. On Red Hat, the panel has several default icons: the main menu (red hat), the Mozilla Web browser (globe with mouse), the Evolution mail tool (envelope), followed by several OpenOffice applications including a word processor and a spreadsheet, the Print Monitor (printer), the Workspace Switcher (squares), and a clock.

To start a program, you can select its entry in the main menu, or access applications through corresponding icons in the Start Here applications window. You can also click its application launcher button in the panel (if there is one), drag a data file to its icon, or select the Run Program entry in the main menu. This opens a small window where you can type in the program name.

8 Chapter 6

X Window System and Graphical Interface

![](bbox=[0.218, 0.065, 0.975, 0.283])

Figure 6-5 A typical window

# Window Manager

A window manager, the program that controls the look-and-feel of the basic GUI, runs on top of a desktop manager and controls all aspects of the windows in the X Window System environment. The window manager defines the appearance of the windows on your desktop, as well as how you operate and position them: open, close, move, resize, iconify, and so on. The window manager may also handle some session management functions, such as how to pause, resume, restart, or end a windowing session (page 183).

A window manager controls window decorations: the titlebar and border of a window. Aside from the aesthetic aspects of changing window decoration, you can alter the functionality by modifying the number and placement of buttons on the titlebar.

The window manager takes care of window manipulation so that the client programs do not need to. This setup is very different from that of many other operating systems, and the way that GNOME and KDE deal with window managers is different from other desktop environments. Window managers do more than manage windows by providing a useful, good-looking, graphical shell to work from. From their open design allows users to define their own policy down to the fine details.

GNOME and KDE are not dependent on any particular window manager and can work with several different window managers. Because of their flexibility, you will not see major parts of your desktop environment change when you switch from one window manager to another. These desktop managers work with a window manager to make your work environment intuitive and easy to use. The desktop manager does not control window placement but does get information from the window manager about window placement.
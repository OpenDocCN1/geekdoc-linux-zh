![](bbox=[0.32, 0.08, 0.66, 0.28])

**FIGURE 6.7** You use switchdesk to set the default window manager for X sessions.

Choosing a window manager is a matter of preference, necessity, or policy. You might prefer to use one of the older window managers—such as the Tab Window Manager (*twm*) or the Motif Window Manager (*mwm*)—on legacy PCs because they have fewer system resource requirements (that is, they require less hard drive space, CPU horsepower, and system memory). Newer desktop environments require 64MB or even more memory for good performance. The following sections describe some of the most popular window managers and their uses.

# # The Tab Window Manager (*twm*)

The Tab Window Manager (*twm*), which is included with Xorg and also sometimes known as Tom’s Window Manager, is a legacy client that provides modest but essential features in a small (less than 1MB) memory footprint. It supports window decorations, menus, icons, and other features, but it does not support virtual desktops, session management, and other features, such as drag and drop.

The *twm* window manager is used as a fallback, or *failsafe*, window manager for Fedora as it requires much less video and system memory. It is included with the Xorg software distribution and will be used as your window manager after you log in or start X in the event the system or your default window manager settings are lost or unusable. The *twm* resource file, *system.twmrc*, is located under the */etc/X11/twm* directory. You can configure this file to provide a default desktop with a custom application menu if you save your settings to a file named *.twmrc* in your home directory. The format of this configuration file is documented in the *twm* man page.

A sample *twm* desktop is shown in Figure 6.8, displaying the *xosview*, *xclock*, *xcalc*, and *xterm* clients. The default desktop color can be changed using the *xsetroot* client. You access the desktop menu in *twm* by left-clicking in a blank area of the main window, known as the *root* display.
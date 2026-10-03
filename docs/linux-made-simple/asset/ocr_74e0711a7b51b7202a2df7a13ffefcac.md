# Desktops

Gnome, KDE Cinnamon, Unity – we’ll just call it the user interface.

If you consider the kernel to be the lowest level of the system, the highest level is the user interface. Everything else, from the kernel through the drivers and hardware interfaces, is of no use until you can use the computer. This generally means a graphical desktop, and here we come across more layers. X (or maybe Wayland in the future) simply provides a blank canvas. You then need something to provide the niceties of a windowed interface, and that something is the window manager.

In the past, window managers were standalone systems, and there are still plenty of these available, such as OpenBox or Enlightenment, but nowadays they are often part of a larger desktop environment. Strictly speaking, a window manager is responsible for the handling of windows on the desktop, their opening, closing, placement and other manipulations. Over time, they grew to incorporate other features, such as taskbars and program launcher menus, until they developed into desktop environments.

# Software collections

A desktop environment is simply a more or less integrated collection of utilities to provide the features needed to run a complete desktop. Running programs, manipulating their windows, keeping track of what is going on and enabling programs to communicate with one another are all features of desktop environments, but they still have a window manager at their heart – KWin for KDE and Metacity in Gnome to name but two.

What sets a desktop environment apart from a window manager is the level of integration. This is

![](bbox=[0.075, 0.37, 0.255, 0.6])

![](bbox=[0.57, 0.2, 0.9, 0.35])

> There are also plenty of lightweight window managers, like OpenBox running on CrunchBang here.

particularly evident in KDE, where everything works around a common core, and programs not only communicate with one another, but an instance of one program can even be embedded in the window of another.

While it may not make much sense to use KWin on Gnome, you may want to try one of the more specialist window managers that offer greater control over window handling, or use a different method of displaying them. There are tiling window managers, like awesome and xmonad, that resize windows so they all fit on the desktop (KDE has its own option to behave like this). There are also window managers designed to be controllable with the keyboard, and minimal window managers that are useful for specialist systems that run a single program in a full-screen window and don’t want any widgets cluttering up the place.

![](bbox=[0.225, 0.61, 0.9, 0.92])

> Gnome, KDE, Unity, Cinnamon, Mate – we aren’t exactly short of choice when it comes to desktop environments, but how many of you have tried more than a couple?
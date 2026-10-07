# CHAPTER 24 Kernel and Module Management

![](bbox=[0.1865, 0.0935, 0.8135, 0.4335])

FIGURE 24.2 The make menuconfig utility, a small improvement over make config.

In make menuconfig, you use the arrow keys to move the selector up and the spacebar to move the focus at the bottom of the screen to either Select, Exit, or Help.

If a graphical desktop is not available, menuconfig is the best you can do. However, both of these utilities offer an improvement over editing the config file directly, but if you want to configure the kernel through a true graphical interface—with mouse support and clickable buttons—make xconfig is the best configuration utility option. To use this, you must have the X Window System running. The application xconfig is really nothing but a Tcl/TK (a Window widget providing borders, menus, dialog boxes, and the like) interface used to wrap around data files that are parsed at execution time. Figure 24.3 shows the main menu of xconfig for the 2.4.19 kernel.

After loading this utility, you use it by clicking on each of the buttons that list the configuration options. Each button you click opens another window that has the detail configuration options. Three buttons are at the bottom of each window; Main Menu, Next, and Prev(ious). Clicking the Main Menu button closes the current window and displays the main window. Clicking Next takes you to the next configuration section.

## FIGURE 3-1 The Bluecurve GNOME desktop

mouse button. To create a link, right-click the item and select Make Link from the pop-up menu. You can then drag the link wherever you wish.

The panel also contains a workspace switcher for virtual desktops, which appears as four squares. Clicking a square moves you to that area. You can configure your GNOME interface, setting features such as the background, by using the Preferences items listed either on the main menu Preferences entry or the Preferences window within the Start Here window. Click the image of a compass with a map on the desktop to open the Start Here window. To configure system settings such as adding users, installing printers, and setting up network connections, open the System Settings window, accessible from the Start Here window, or select the System Settings menu.

To quit the GNOME desktop, select the Log Out entry at the bottom of the main menu. If you entered from a login window, you are then logged out of your account and returned to the login window. If you started GNOME from the command line, you are returned to the command line prompt, still logged into your account.

## KDE

The K Desktop Environment (KDE) with Bluecurve looks much like GNOME with Bluecurve as shown in Figure 3-1, with the addition of icons for your CD-ROMs and floppy drives.

It displays a panel at the bottom of the screen that looks very similar to one displayed on the GNOME desktop. The file manager appears slightly different but operates much the same way as the GNOME file manager. It is also Internet-aware and can operate as a Web browser. There is also a Control Center entry in the main menu that opens the KDE control center, from which you can configure every aspect of the KDE environment, such as themes, panels, peripherals like printers and keyboards (already handled by Red Hat system tools), even the KDE file manager’s Web browsing capabilities.

## Window Managers for Linux

Though GNOME and KDE are wholly integrated desktops, they, in fact, interact with the operating system through a window manager, Metacity in the case of GNOME and the KDE window manager for KDE. You can use a different GNOME- or KDE-compliant window manager if you wish, or simply use a window manager in place of either KDE or GNOME. You can think of a window as taking the place of a command line. Operations you perform through the window are interpreted and sent to the Linux system for execution. Window managers operate off the underlying X Window System, which actually provides the basic window operations that allow you to open, move, and close windows as well as display menus and select icons. Enlightenment and AfterStep manage these operations, each in its own way, providing their own unique interfaces. The advantage of such a design is that different window managers can operate on the same Linux system. In this sense, Linux is not tied to one type of graphical user interface (GUI). On the same Linux system, one user may be using the Window Maker window manager, another may be using the Afterstep window manager, and still another the Enlightenment window manager, all at the same time. You can find out detailed information about different window managers available for Linux from the X11 Web site at www.xwinman.org. The site provides reviews, screenshots, and links to home sites, as well as a comparison table listing the features available for the different window managers.

## Command Line Interface

When using the command line interface, you are given a simple prompt at which you type in your command (see Chapter 8). Even with a GUI, you sometimes need to execute commands on a command line. Linux commands make extensive use of options and arguments. Be careful to place your arguments and options in their correct order on the command line. The format for a Linux command is the command name followed by options, and then by arguments, as shown here:

```
$ command-name options arguments
```

An option is a one-letter code preceded by one or two hyphens, which modifies the type of action the command takes. Options and arguments may or may not be optional, depending on the command. For example, the ls command can take an option, -s. The ls command displays a listing of files in your directory, and the -s option adds the size of each file in blocks. You enter the command and its option on the command line as follows:

```
$ ls -s
```

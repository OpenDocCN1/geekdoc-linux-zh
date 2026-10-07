
# CHAPTER 6 The X Window System

After you press Enter, a file named XF86Config.new is created in root's home directory, the /root directory. You can use this file for a test session, like this:

```
# XFree86 -xf86config / /root/XF86Config.new
```

# Starting X

You can start X sessions in a variety of ways. Normally, the Red Hat Linux installer sets up the system's initialization table /etc/inittab to have Linux boot directly to an X session using a display manager (that is, a client that provides a graphical login). After the user logs in, or if she boots to a local session, or if the system is properly configured, to an X session that is running on a remote computer on the network. Logging in via a display manager requires a user to enter a username and password. You can also start X sessions from the command line. The following sections describe these two methods.

# Using a Display Manager

A X display manager presents a graphical login that requires a username and password to be entered before access is granted to the Red Hat desktop. It also allows you to choose a different desktop for your X session. Whether or not an X manager is presented after you boot Red Hat is controlled by a runlevel—a system state entry in /etc/inittab. Red Hat Linux defines the following runlevels in the file:

```
# 0 (Do Not set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do Not set initdefault to this)
```

Runlevel 5 is used for multiuser with a graphical X login via a display manager; booting to runlevel 3 provides a console, or text-based, login. The initdefault file /etc/inittab determines the default runlevel:

```
id:5:initdefault:
```

In this example, Red Hat Linux boots and ends up running X.
The default display manager might also be specified in /etc/inittab:

```
x:5:respawn:/usr/bin/xdm -nodaemon
```

However, Red Hat Linux uses a shell script named prefdm, found under the /etc/X11 directory, to set the display manager:

```
x:5:respawn:/etc/X11/prefdm -nodaemon
```

According to this script, the display manager is based on the file named desktop under the /etc/sysconfig directory. The words GNOME, KDE, and XDM following DESKTOP= entry determine what display manager is used for login. The following sections describe how to configure the three most used display managers: gdm, kdm, and xdm.

# Configuring gdm

The gdm display manager is part of the GNOME library and client distribution included with Red Hat Linux. The gdm display manager provides a graphical login when a system boots directly to X. Its login (which is actually displayed by the gdmlogin client) drop-down menus of window managers, languages, and system options for shutting down (halting) or rebooting the workstation. Although you can edit (as root) gdm.conf under the /etc/X11/gdm directory to configure gdm, a much better way to configure GNOME's display manager is to use the gdmconfig utility.

You can use the gdmconfig utility, shown in Figure 6.5, to configure many aspects and features of the login display. You launch this from the GNOME desktop panel System Login Screen item, or from the command line, like this:

```bash
# gdmconfig &
```

After you press Enter, you see the GDM Setup window, as shown in Figure 6.5.

![](img/446debe023486a07fde575245cf7a3ff_228_0.png)

FIGURE 6.5 You use gdmconfig to configure the gdmlogin screen when using gdm as a display manager.

You can specify settings for security, remote network logins, the X server, and session chooser setup by clicking on the tabs in the GDM Setup dialog.

# Configuring kdm

The kdm client, which is part of the KDE desktop suite, offers a similar graphical login to gdm. You configure kdm by running the KDE Control Center client kcontrol, as the root operator, like so:

```bash
$ su -c kcontrol
```

After you enter the root password, the Control Center appears. In the Index tab of the left of the KDE Control Center window, you click the System menu to open the System contents, and then you double-click the Login Manager menu item. The right pane of the Control Center window displays the tabs and configuration options for the kdm Login Manager, as shown in Figure 6.6.

![](img/446debe023486a07fde575245cf7a3ff_229_0.png)

**FIGURE 6.6** You configure kdm by choosing tabs and settings in the Control Center dialog box.

You can click on the Control Center dialog box to set configuration options. Options in these tabs allow you to configure the login display, prompts, user icons, session management, and configuration of system options (for shutting down or rebooting). After you have made your configuration choices in each tab, click the Apply button to have the changes immediately; otherwise, the changes are applied when the X server restarts.

# Using the xdm

The xdm display manager is part of the FreeX86 distribution and offers a bare-bones login for using X. Although it is possible to configure xdm by editing various files under the /etc/X11/ directory, GNOME and KDE offer a greater variety of options in display manager settings. The default xdm login screen's display is handled by the xsetroot client, which is included with XFree86, and Owen Taylor's xsri client, as specified in the file Xsetup_0 in the xdm directory /etc/X11. The xsri client is used to set the background color of the login display's desktop and to place an image of Red Hat's logo in the upper-left corner of the display.

# Starting X from the Console by using

If you have Red Hat set to boot to runlevel 3, a text-based console login, you can start an X session from the command line. You use the startActivity command (which is actually a shell script) to do so. You launch the X server and an X session by using startx, like this:

```bash
$ startx
```

startX first looks in your home directory for a file named .xinitrc. This file can contain settings that will launch an alternative desktop and X clients for your X session. The default system .xinitrc is found in the /etc/X11/xinit directory, but a local file can be used to customize an X session and launch defaults. For example, you can download and install the mlwm window manager, which is available from http://www.w2u.biglobe.ne.jp/~y-miyata/mlwm.html in the /usr/local/bin directory. You can then use the mlwm desktop for your X session, the xterm terminal client creating a .xinitrc file containing the following:

```bash
xterm &
exec /usr/local/bin/mlwm
```

Using a custom .xinitrc is not necessary if you're using Red Hat's desktop, which runs X and either a GNOME-aware window manager or KDE as a desktop environment.

You can also use the startActivity command with one or more command-line options. These options are passed to the X server before it launches an X session. For example, you can use startx to specify a color depth for an X session using the -depth option, followed by a number as 8, 16, 24, or 32 for 256, thousands, or millions of colors (as defined in the X configuration file and if supported). Using different color depths can be useful during development, for testing how X clients look on different displays, or to conserve of video memory, such as when trying to get the highest resolution (increased color depth can sometimes affect the maximum resolution of older video cards).

For example, to start a session with thousands of colors, you use the startActivity command like:

```bash
$ startx --depth 16
```

Another option that can be passed is a specific dots-per-inch (dpi) resolution that is to be used for the X session. For example, to use 100 dpi, use the -dpi option followed by one, like this:

```bash
$ startx -dpi 100
```

# CHAPTER 6 The Window System

You can also use startx to launch multiple X sessions. To start the first X session, you use startx followed by a display number and virtual console. The default console used for X is 7, so you can start the session like:

```bash
$ startx :0 vt7
```

After X starts and the window manager appears, you press Ctrl+F2 and then log in. Next, you start another session like this, specifying a display number and virtual console:

```bash
$ startx :1 vt8
```

Another X starts. To jump to the first session, you press Ctrl+F7. You use Ctrl+F8 to return to the second session. If you exit the current session and go to another text-based login or shell, you use Alt+F7 or Alt+F8 to jump to the desired session.

Using startx is a flexible way to launch X sessions, but multiple sessions can be confusing, especially to new users, and are a drain on a system that does not have enough CPU horsepower and memory. A better approach is to use multiple workspaces, as known as virtual desktops, as discussed in the following section.

# Selecting and Using X Window Managers

A window manager is launched immediately after the X server starts. The window manager handles the drawing and display of graphical session windows and their onscreen controls. Without a window manager, X client windows cannot be moved over the screen, resized, minimized or maximized, and so on.

Many different window managers are available for Red Hat Linux, providing a number of choices for how the desktop appears and functions.

A window manager provides an X display and customized desktop by handling window decoration, movement, placement, and resizing operations. A window manager can also handle icons, and it can support icon-docking and other window operations as tiling and overlays. Another important window manager task is focus policy—how and when a window becomes active. A window becomes active when the pointer is over it, for example, or it might require a mouse click for activation.

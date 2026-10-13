
## Mode selection

You can select two types of modes: pixel dimensions and color depth. The XF86Setup utility allows you to select pixel dimensions from 320×200 to 1600×1200. It allows you to select color depth in bits: 8, 16, 24, or 32.

> If you select more than one graphics mode, you can switch between these modes using the Ctrl+Alt+Num+ and Ctrl+Alt+Num- commands. Num+ and Num- are the plus and minus keys on the numeric keypad. Using this method assumes the Allow Video Mode Switching option is enabled as described in the next section.

## Other

The two key options in this section are Allow Server To Be Killed With Hotkey Sequence Ctrl+Alt+Backspace and Allow Video Mode Switching. The first option allows you to exit the X Server by pressing the noted keys. That option returns you to the command-line interface or an X login window, depending on the level set as initdefault in your /etc/inittab configuration file.

## Xconfigurator

Red Hat Linux has its own set of graphical configuration utilities including Xconfigurator, mouseconfig, and kbdconfig. Although they're released under the General Public License (GPL), they are generally available only on Red Hat and derived distributions.

You can configure the X Window, or X11, with Xconfigurator nearly as well as with XF86Setup. If your mouse doesn't work, you can use the Tab, Arrow, Page Up, Page Down, and Spacebar keys to navigate Xconfigurator's menus. The database of video controllers and monitors is somewhat limited: You can set up a custom monitor with the same criteria as used on other utilities.

> Don't exceed the horizontal or vertical refresh capabilities of your monitor. When prompted, don't probe your video controller. Select the amount of memory available on your video card from the available menu. Also don't select a clock chip; the X Server can set this when you start the X Window.

## SaX

S.u.S.E. has its own graphical configuration utility known as SaX. You can start it from a command-line interface or one of the S.u.S.E. menus. SaX is divided into five sections: mouse, keyboard, card, monitor, and desktop. SaX is almost as complete as the XF86Setup utility.

## Window Managers

Window managers determine what you see in a GUI desktop. As strange as it sounds, a window manager is also an application. Linux window managers don't interface directly with the kernel; you can shut down any window manager without shutting down Linux.

The following sections provide a brief overview of seven different window managers. There are several dozen window managers that you can configure and install on your Linux computer. If you're familiar with Linux, you've probably heard about at least two of these window managers: GNOME and KDE.

Linux window managers can be divided into three categories. The first window managers, such as fvwm, include a minimum of frills, which keeps them simple. They demand little in resources. A second group emphasizes customizability; these window managers include Enlightenment, AfterStep, WindowMaker, and Blackbox. The third group's window managers, which include GNOME and KDE, contain their own login screens, applications, icons, menu bars, and so on for a complete desktop package.

### GNOME

GNOME is a complete desktop package, which includes utilities such as a package manager, pop-up menus, and other utilities. GNOME applications include an office suite, financial programs, and more. It is based on the GTK+ widget library, which is released under the GPL. As of this writing, GNOME is the default window manager for Red Hat Linux.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_216_0.png)

> GNOME also includes a display manager, used in place of xdm, to manage logins. You can set up the GNOME display manager to log in to a window manager other than GNOME.

### KDE

Like GNOME, KDE is a complete package, which includes utilities such as a control panel, package manager, taskbar with icons, and pop-up menus. KDE applications include an office suite, a package manager, and a mail reader. KDE is based on the Qt widget library, which was recently relicensed under the GPL. It is perhaps the window manager that most closely resembles Microsoft Windows in its look and feel. As of this writing, KDE is the default window manager for Corel, S.u.S.E., and Caldera Linux.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_217_0.png)

KDE also includes a display manager, used in place of xdm, to manage logins. You can set up the KDE display manager to log in to a window manager other than KDE.

### fvwm

The fvwm window manager was the standard before the development of KDE and GNOME. Because it requires a relatively small amount of memory, it was popular in an age when memory was more expensive. Most of its options are contained in the pop-up menus. Version 2 of fvwm updated the look and feel of this GUI. A later version known as fvwm95 was designed to look something like Microsoft Windows 95.

### Enlightenment

As of this writing, the Enlightenment window manager is a work in progress. Other window managers borrow code from each other, whereas Enlightenment is unique. It's designed to be the most configurable of window managers, which makes it more suitable for users who aren't satisfied with any other window manager. It is usually installed on higher-end workstations for users who need the power, not for their window manager, but for their graphical applications.

### AfterStep

Although the AfterStep window manager is based on fvwm code, it is designed to look like the GUI for the NeXTStep operating system. Originally designed for the NeXT workstation, NeXTStep was designed to be a more intuitive GUI. NeXT was developed by Apple engineers who wanted to extend the user friendliness of the Macintosh operating system.

AfterStep includes a “wharf” of icons, which allows you to launch programs seemingly like a pictorial version of the Microsoft Windows Start menu.

### WindowMaker

The WindowMaker window manager is similar in feel to AfterStep. As an official part of the GNU project, its developers are currently incorporating GNOME features into its GUI.

### Blackbox

The Blackbox window manager is designed to run in a minimum of RAM. Images are cached after they're drawn on your screen. Unlike many of the other window managers, Blackbox includes support for KDE, but not for GNOME applications.

## Window Manager Commonalities

There are a wide variety of Linux window managers. As discussed in the previous sections, each window manager has a number of special features. Even though this chapter does not review all available Linux window managers, all window managers share some commonalities. They have virtual displays. You can copy and paste text between different windows. In addition, within individual X Windows, you can scroll up and down a file, resize the window, or change the size of the font.

Several window managers make it possible to incorporate features and applications from the GNOME and KDE packages.

### Virtual Displays

With most GUIs, what you see on the monitor is all the display room that you get. To get more room in other GUIs, you need another monitor. With the Linux X Window, most window managers actually include several virtual displays. You can switch between displays by clicking on a pager, which moves you from one virtual display to another.

An example of a virtual display pager is shown in Figure 10.5 on the right. The numbers 1, 2, 3, and 4 signify the virtual displays available in this window manager.

### Hidden Windows

If you can't find a window that's open or you think your system is "locked," there are a couple of things that you can try before you close your X Window. Your window may only be hidden; pressing the Alt+Tab keys toggles you between available windows. Your window may be in another virtual display; try clicking the other pages of the virtual display pager.

### Copy and Paste

As of this writing, Linux window managers don't include a regular clipboard that allows you to copy and paste between applications. But you can copy text

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_218_0.png)

Figure 10.5 Window manager taskbars often include pagers.

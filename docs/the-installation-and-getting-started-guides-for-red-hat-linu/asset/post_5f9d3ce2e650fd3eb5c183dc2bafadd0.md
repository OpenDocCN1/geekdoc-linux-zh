
## The Getting Started Guide for Red Hat Linux 6.0

application you minimized in the task list on the right side of the GNOME Pager. Press the button for that application and it will return to your desktop.

![](img/46f4935125ba89e12897afbe9d77a097_543_0.png)

You may read more about the GNOME Pager in the section called GNOME Pager in Chapter 12.

The following sections go into more detail, describing each component of the system.

## 3 Window Managers and GNOME

### About Window Managers

The window manager is the piece of software that controls the windows in the X window environment. The placement, borders, and decorations of any window are managed by the window manager. This is very different from many other operating systems, and the way GNOME deals with window managers is different from other desktop environments.

As stated earlier in this guide, GNOME is not dependent on any one window manager. This means that major parts of your desktop environment will not change when you decide to switch window managers. GNOME works with the window manager to give you the easiest work environment you can have. GNOME does not worry about window placement but gets information from the window manager about their placement. The GNOME Pager will only work with a GNOME compliant window manager that will drag and drop on the desktop.

At the time of this version of the GNOME User's Guide the Enlightenment Window Manager is the only window manager that is 100% compliant. There are many other window managers that are partially compliant or are being worked on to meet compliance.

Some of the window managers that have partial to full compliance at the time of this version of the GNOME User's Guide are:

- Enlightenment - http://www.enlightenment.org
- Icewm - http://www.kiss.uni-lj.si/~k4fr0235/icewm/
- Window Maker - http://www.windowmaker.org
- FVWM - http://www.fvwm.org/

### Changing Window Managers

At any time you may change the window manager you are using by utilizing the Window Manager Capplet in the GNOME Control Center. You may read more about this Capplet in the section called *Window Manager Capplet* in Chapter 10.

**IMPORTANT:** Keep in mind that the window manager you choose to use may not be compliant with GNOME and you may not benefit from some of GNOME features if you use it.

## 4 The Enlightenment Window Manager

### Introduction

GNOME is a desktop environment that is not dependent on any one window manager in order to control how applications and other features interact with each other. GNOME can work with a variety of window managers. The window manager is what controls the window borders, window decorations, and the functionality of those windows. Currently there are about three or four window managers that are considered GNOME compliant. Being GNOME compliant means much more than simply being able to run with GNOME; it also means being aware of GNOME and what GNOME offers. This includes session management, desktop settings, and interactivity with applications such as the GNOME Pager.

The Default Window Manager for this release of Red Hat Linux is a window manager called Enlightenment. Within Enlightenment there is a tool which will help you to configure the window manager to your specifications.

### The Enlightenment Configuration Tool

There are two ways to launch the Enlightenment Configuration tool (E-conf). You may open the GNOME Control Center and select the Window Manager Capplet from the Desktop group. If you have Enlightenment as your current window manager you may run E-conf by pressing the Run Configuration Tool for Enlightenment button.

You may also launch E-conf by clicking your middle mouse button (or both right and left mouse buttons if you have emulation) on the desktop and selecting the Enlightenment Configuration item from the pop-up menu.

E-conf is divided into many sections that control various effects and functions within Enlightenment (E). You will find a list of these sections


![](img/b22364e57409c2481ba806e4e6b9309c_149_0.png)

Figure 3-20: Use the Display Settings window to configure basic desktop, video card, and monitor settings.

Changes made in the Display Settings window result in the creation of a new /etc/X11/xorg.conf file. The next section describes what the xorg.conf file contains.

> **TIP:** If the Display Settings window fails to create a working *xorg.conf* file, you can try another approach. With no GUI on as root user, type the following commands from a shell:
>
> ```
> # Xorg -configure
> # X -xf86config /root/xorg.conf.new
> ```
>
> The first line creates *xorg.conf.new* in the /root directory. The second tries to start your GUI with that new config file. If the GUI works, copy /root/xorg.conf.new to /etc/X11/xorg.conf. You may need to run *system-config-mouse* to get the mouse working properly after this.

## Understanding the xorg.conf file

Beginning with Fedora Core 2, the XFree86 X server was replaced by the X server from X.Org. Although that change should be invisible to most users, if you like to change X settings directly, you need to know that the main X configuration file is now /etc/X11/xorg.conf and not /etc/X11/XF86Config.

The xorg.conf file (located in the /etc/X11/ directory) contains definitions used by the X server to use your video card, keyboard, mouse, and monitor. In general, novice users should not edit this file directly. For some video cards, however, manual configuration may be required to get the card working properly.

The following is a description of the basic information contained in the *xorg.conf* file:

- **ServerLayout section** — Binds input and output devices for your X session. Lets you set server definitions for different X servers (if necessary).
- **Module section** — Describes which X server modules should be loaded.
- **Files section** — Sets the locations of the RGB (color), modules and fonts databases.
- **InputDevice sections** — Separate sections identify keyboard and mouse input devices.
- **Monitor section** — Sets the type of monitor, along with its horizontal sync rate, vertical refresh rate, and settings needed to operate at different resolutions.
- **Device section** — Identifies your video card and, optionally, video RAM and clock information for the chipset.
- **Screen section** — Binds the graphics board and monitor information to be referenced later by the ServerLayout section.
- **Keyboard section** — Sets keyboard settings, including the layout of the keyboard and the way certain key sequences are mapped to the keyboard.
- **Pointer section** — Selects the pointer you are using (typically a mouse linked to `/dev/mouse`). Also sets speed and button emulation, when appropriate.
- **DRI** — Provides information for Direct Rendering Infrastructure (used for accelerated 3D graphics).

### Configuring video cards for gaming

Some games and video players require special features to work properly (or at all, in some cases). For games that require 3D hardware acceleration, including some that run under TransGaming's WineX, TransGaming recommends using NVIDIA GeForce Graphics cards.

Because only basic NVIDIA video card drivers are included in Fedora (NVIDIA's own drivers are not open source), you need to get NVIDIA drivers yourself to use those cards for gaming. You can download NVIDIA drivers for Linux from `www.nvidia.com/object/linux_display_archive.html`.

Select the latest drivers from the list (look for version 1.0-5336 or later). Download and install the drivers as described.

Games that don't require 3D hardware acceleration should work fine with most video cards that are supported by the X.Org X server drivers.

> **TIP:** To use hardware DRI acceleration on Voodoo 3 cards, you must have your display set to use 16bpp resolution. On Voodoo 5 cards, only 16bpp and 24bpp resolutions are supported.

### Getting more information

If you tried configuring X and you still have a server that crashes or has a garbled display, your video card may either be unsupported or may require special configuration. Here are several locations you can check for further information:

- **X.Org** (www.x.org) — The latest information about the X servers that come with Fedora is available from the X.Org Web site. X.Org is the freeware version of X recently used by many major Linux distributions to replace the XFree86 X server.
- **Red Hat Support** (www.redhat.com/apps/support/) — Search the Red Hat support database for the model of your card. There may already be reports of problems (and hopefully fixes) related to your card.
- **X documentation** — README files that are specific to different types of video cards are delivered with the X.Org X server. Visit the X doc directory `/usr/X11R6/lib/X11/doc` for a README file specific to the type of video card (or more specifically, the video chipset) you are using. A lot of good information can also be found on the xorg.conf man page (type `man xorg.conf`).

### Summary

The X Window System provides the basis for most graphical user interfaces available for Fedora and other Linux systems today. Although X provides the framework for running and sharing applications, the GNOME and KDE desktop environments, along with a window manager and theme, provide the look-and-feel of your desktop.

Using various configuration files and commands, you can change nearly every aspect of your graphical environment. Backgrounds can be assigned a single color or can be filled with single or tiled graphic images. Menus can be changed or enhanced. Multiple virtual workspaces can be used and managed.

After reading this chapter, you should feel comfortable working with the GNOME and KDE desktops. The next chapter should help you work from the traditional command line interface, referred to as the shell.

## Chapter 4: Using Linux Commands

### In This Chapter

- Understanding the Linux shell
- Using the Linux shell
- Working with the Linux file system
- Using the vi text editor in Linux

This chapter presents a view of Linux from the shell. The *shell* is a command-line interpreter that lets you access some of the most critical Linux tools. The shell is powerful, complex, and almost completely intuitive.

Although at first it isn't obvious how to use the shell, with the right help you can quickly learn many of the most important shell features. This chapter is your guide to working with the Linux system commands, processes, and file system from the shell. It describes the shell environment and helps you tailor it to your needs. It also describes how to use and move around the file system.

### The Shell Interface

Throughout this book, there are procedures that require you to use a shell to run commands. How you first get to a shell depends on whether your computer is configured to have a graphical user interface (GUI) or not. A desktop system, by its nature, starts with a GUI. Server systems often are run entirely from the command line. Here are ways of reaching a shell, depending on whether you have a desktop GUI running or not:

- **No desktop** — If your Linux system has no GUI (or one that isn't working at the moment), you log in from a text-based prompt and immediately begin working from the shell.
- **With desktop** — With the desktop GUI running, you can open a Terminal window (right-click on the desktop, then click Open Terminal) to start a shell. You can begin typing commands into the Terminal window.

If you are using a shell interface, the first thing you see is the shell prompt. The default prompt for a normal user is simply a dollar sign:

$

The default prompt for the root user is a pound sign (also called a hash mark):

#

For most Linux systems, the $ or # prompts are preceded by your user name, system name, and current directory name. So, for example, a login prompt for the user named jake on a computer named pine with /tmp as the current directory would appear as:

{jake@pine tmp}$

You can change the prompt to display any characters you like. You could use as your prompt the current directory, the date, the local computer name, or any string of characters. (To configure your prompt, see the “Setting your prompt” section later in this chapter.)

Although there are a tremendous number of features available with the shell, it’s easy to begin by just typing a few commands. Try some of the commands shown in the remainder of this section to become familiar with your current shell environment.

In the examples that follow, the $ or # symbols indicate a prompt. The prompt is followed by the command that you type and then by Enter or Return (depending on your keyboard). The lines that follow show the output that results from the command.

### Checking your login session

When you log in to a Linux system, Linux views you as having a particular identity. That identity includes your user name, group name, user ID, and group ID. Linux also keeps track of your login session: it knows when you logged in, how long you have been idle, and where you logged in from.

To find out information about your identity, use the id command as follows:

```
$ id
id=501(chris) gid=105(sales) groups=105(sales),4(admin),7(lp)
```

This shows that the user name is chris, which is represented by the numeric user ID (uid) 501. Here, the primary group for chris is called sales, which has a group ID (gid) of 105. Chris also belongs to other groups called adm (gid 4) and lp (gid 7). These names and numbers represent the permissions that chris has to access computer resources. (Permissions are described later in this chapter in the section on working with files.)

You can see information about your current login session by using the who command. In the following example, the -m option tells the who command to print information about the current user, -u says to add information about idle time and the process ID, and -H asks that a header be printed:

```
$ who -umH
NAME		LINE		TIME		IDLE		PID	COMMENT
chris	tty1		Jan 13 20:57	-		2013
```

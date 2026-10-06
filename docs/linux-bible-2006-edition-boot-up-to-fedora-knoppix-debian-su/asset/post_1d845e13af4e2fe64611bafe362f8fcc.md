
# Chapter 3 Getting into the Desktop

- $HOME/.xinitrc — The .xinitrc file is used to let individual users set up their own desktop startup information. Any user can add a .xinitrc file to his or her home directory. The result is the contents of that file will override any system-wide settings. If you create your own .xinitrc file, it should have as its last line exec windowmanager, where windowmanager is the name of your window manager; for example:

```
exec /usr/X16/bin/blackbox
```

Slackware has at least seven window managers from which you can choose, making a good place to try out a few. It also includes a tool called wmconfig which changes the window manager system-wide (in the /etc/X11/xinit/xinitrc file). To use that tool, as the root user simply type xwmconfig any on a Slackware system. Figure 3-15 shows an example of that screen.

![](img/a2d958d7eab32ca5b89b2b8af808aa70_150_0.png)

**Figure 3-15:** In Slackware, you can change window managers using the xwmconfig command.

Select the window manager you want to try from that screen and select OK. That window manager will start the next time you run startx (provided you don't override it by creating your .xinitrc file). Here are your choices:

- **Xfce (www.xfce.org)** — The xfce window manager is designed to be lightweight and fast.

- **Blackbox (www.blackbox.sourceforge.net)** — Another lightweight window manager that strives to require few library dependencies so it can run in many environments. Offers many features for setting colors and styles.

- **FluxBox (http://fluxbox.sourceforge.net)** — Based on Blackbox (0.6.1), FluxBox adds nice features such as tabs (where you can join multiple windows as they appear as multiple tabs a a single window). It also includes an icon bar and adds some useful mouse features (such as using your mouse wheel to change workspaces).

- **Window Maker (www.windowmaker.org)** — Window Maker is a clone of the NEXTSTEP graphical interface, a popular UNIX workstation of the 1980s and 1990s. It is a particularly attractive window manager, with support for themes, various window decorations, and features for creating backgrounds, animations, and adding aliases (called docaps).

- **FWWM (www.fwwm.org)** — This window manager supports full internationalization, window manager hints, and improved font features. Interesting features include window shading in all directions (even diagonal) and side titles (including text displayed vertically).

- **FWWM-95 (http://fwwm95.sourceforge.net)** — A version of FWWM was created to look and feel like Windows 95.

- **Twm (The Window Manager)** — Although no longer actively maintained, some people still use twm when they want a truly bare-bones desktop. Until you click the left button in twm, there's nothing on the screen. The menu pops up to open and close windows.

There are many other window managers available for Linux as well. To check out more, visit the Xwinman Web site (www.plig.org/xwinman).

Once the default is set for your window manager, users can set their own window manager to override that decision. The following section describes how to do that.

## Choosing Your Personal Window Manager

Simply adding an **exec** line with the name of the window manager you want to use to your own .xinitrc file in your home directory startx to start your window manager for you. Here is an example of the contents of a .xinitrc to start the Window Maker manager:

```
exec /usr/bin/wmaker
```

Make sure that the file is executable (chmod 755 $HOME/.xinitrc). The Window Maker window should start before you start your desktop. Other window managers you can choose include Blackbox (/usr/X11R/bin/blackbox), FluxBox (/usr/X11R/bin/fluxbox), FWWM (/usr/X11R/bin/fluxbox), FWWM-95 (/usr/X11R/bin/fwwm95), and twm (/usr/X11R/bin/twm).

## Getting More Information

If you tried configuring X and will still have a server that crashes or has a garbled display, your video card may be unsupported or may require special configuration. Here are a couple of locations you can check for further information:

- **XOrg (www.x.org)** — The latest information about the X servers that come with Fedora is available from the XOrg Web site. XOrg is the freeway of X version used by many Linux distributions to replace XFree86 X.

- **X documentation** — README files specific to different types of video cards are delivered with the XOrg server. Visit the *doc* directory (/usr/X11/lib/doc) for a README file specific to the type of video card (or more specifically, the video chipset) you are using. A lot of good information can also be found on the **xorg.conf** man page (**xorg.conf**).

## Summary

Complete desktop environments that run in Linux can rival desktop systems from any operating system. KDE and GNOME are the most popular desktop environments available for Linux. For people who want a sleeker, more lightweight desktop environment, a variety of simple window managers (Blackbox, FVWM, twm, FluxBox, and many others) are available to use in Linux as well.

The KDE desktop is well known for its large set of applications (office productivity tools, games, multimedia, and other applications). GNOME and KDE desktops that aren't changed much from how they are delivered from those desktop projects. Other Linux systems (such as Slackware and Gentoo) have their own look-and-feel over GNOME and KDE desktops.

While the latest Windows systems won't run on any older 486 and 280 machines, you can use an efficient Linux system such as Slackware, add a lightweight window manager, and get reasonably good performance with your desktop system on those machines.

# Running the Show

In This Part

- Chapter 4 Learning Basic Administration
- Chapter 5 Getting on the Internet
- Chapter 6 Securing Linux

# Learning Basic Administration

Linux, like other UNIX systems, was intended for use by more than one person at a time. Multiuser features enable many people to have accounts on a single Linux system, with their data kept secure from others. Multitasking enables many people to run programs on the computer at the same time. Sophisticated networking protocols and applications make it possible for a Linux system to extend its capabilities to network users and computers around the world. The person assigned to manage all of this is called the *system administrator*.

Even if you are the only person using a Linux system, system administration is still set up to be separate from other computer use. To do most administrative tasks, you need to be logged in as the root user (also the *superuser*) or temporarily get permission. Users other than root cannot change, or in some cases even see, some of the configuration information for Linux. In particular, security features such as stored passwords are protected from general use.

Because Linux system administration is such a huge topic, this chapter focuses on the general principles of Linux system administration. In particular, it examines some of the basic tools you need to administer a Linux system for a personal desktop or on a small LAN. Beyond the basics, it also teaches how to work with file systems and monitor the setup and performance of your Linux system.

## Graphical Administration Tools

Many Linux systems come with simplified graphical tools for administering Linux. If you are a casual user, these tools often let you do everything you need to administer your system without editing configuration files or running shell commands.

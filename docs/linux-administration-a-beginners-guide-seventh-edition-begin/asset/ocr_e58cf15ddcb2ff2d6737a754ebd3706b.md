# 90 Linux Administration: A Beginner's Guide

Following are the primary functions of the RPM:

+   - Querying, verifying, updating, installing, and uninstalling software
- Maintaining a database that stores various items of information about the packages
- Packaging other software into an RPM form

# Getting Down to Business

In Chapter 2 we walked through the operating system installation process. Now that you have a working system, you will need to log into the system to carry out the exercises in this and other chapters of the book. Most will implicitly ask you to type a command. Although it might seem obvious, whenever you are asked to type a command, you will have to type it into a console at the shell prompt. This is akin to the command or DOS prompt in Microsoft Windows but is much more powerful.

You can type a command at the shell in several ways. One way is to use a nice, windowed (GUI) terminal; another is to use the system console. The windowed consoles are known as "terminal emulators" (or "pseudo-terminals"), and there are tons of them.

The base Fedora server operating system that you installed in Chapter 2 may or not have given you an option to install a desktop GUI environment, and you would have been thrown into a black login console after the system rebooted. The exercises in Chapter 3 also assumed that you were following along the text-only terminal console. In this software management chapter, you will now have the option to install a GUI desktop environment of your choice.

So without further ado, your first order of business be to install your desktop environment of choice. Some of the options are GNOME, KDE, XFCE, Mate, LXDE, and so on.

To install the GNOME desktop environment that comes with the Fedora Workstation product, type

```
# dnf -y groupinstall "Fedora Workstation"
```

Once the installation is completed successfully, you'll have to set this graphical environment as the new target or runlevel for this system to boot into. Type

```
# systemctl set-default graphical.target
```

Finally, reboot the system to boot into and log into the graphical desktop environment:

```
# reboot
```
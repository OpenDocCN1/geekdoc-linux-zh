
# 404 Understanding How Fedora Cores

## Understanding the GUI startup

The graphical login screen starts at run level 5. When the init process starts up at run level 5, the last line of the /etc/inittab causes init to start the graphical login process. Here's what the last line in the /etc/inittab file looks like (the number 5 denotes run level 5):

```
x:5-respawn:/etc/X11/prefdm -nodamem
```

This line calls init to run /etc/X11/prefdm, a script that starts a specific display manager — gdm, kdm, or xdm — depending on the setting of a variable DISPLAYMANAGER defined in the /etc/sysconfig/desktop file. The display manager is a program responsible for displaying the graphical login window, authenticating users who log in, running initialization at the start of a session, and cleaning up after the session. The display manager processes the display, making it available to the users and cleaning up after the user session.

If the DISPLAYMANAGER variable is not defined, the /etc/X11/prefdm script checks for gdm, kdm, and xdm in that order and runs whichever manager finds first. The end result is you get gdm if you installed GNOME and KDE as your sole desktop. If you install both GNOME and KDE you get gdm by default because the prefdm script looks for if you have both GNOME and KDE installed on your system and you want gdm as the display manager, define the DISPLAYMANAGER variable in the /etc/sysconfig/desktop file like this:

```
DISPLAYMANAGER="KDE"
```

The next time you reboot the system, the kdm display manager runs.

## GNOME display manager (gdm)

The gdm program is a display manager similar to xdm, the X display manager. Like xdm, gdm starts an X server for each local display, displays a login box, and enables the user to log in to the system.

When gdm runs, it reads various parameters from the configuration file /etc/X11/gdm/gdm.conf, which has a structure similar to a Windows IN file. For example, here are a few lines from a typical gdm.conf file:

```
[daemon]
AutomaticLoginEnable=false
AutomaticLogin-
TimedLogin=false
TimedLogin-
TimedLoginDelay=30
Gre=/usr/bin/gdmgreeting
lines deleted...
```

![](img/d9230b719dc0efd80851f363d8c6f571_430_0.png)

![](img/d9230b719dc0efd80851f363d8c6f571_430_1.png)

# Understanding How Core Boots 405

The /etc/X11/gdm/gdm.conf file has many comment lines — these lines begin with a hash mark (#). Labels in square brackets ([...]) identify sections of the file. The different sections in the configuration file control different aspects of the graphical login screen as well as the tasks the user can perform from screen.

You see the term greeter used in the display manager configuration file. Greeter refers to the login screen — the user interface through which the display manager prompts the user to log in to.

Edit the Welcome line in /etc/X11/gdm/gdm.conf to change the message on the graphical login screen. The default message says Welcome to the hostname, which can be somewhat cryptic. You can edit that and change the message to something meaningful with the syntax Welcome=to ABC Corp.

![](img/d9230b719dc0efd80851f363d8c6f571_431_0.png)

Book VI Chapter 1

Performing Basic Administration

## GNOME session startup under gdm

For the default configuration after a typical Fedora Core installation with the GNOME desktop, gdm manages the login session as:

- 1. The gdm program starts the X server and looks for a script named the local display (for the first display, the filename is :0) in the /etc/X11/gdm/init directory. If it does not find file, gdm executes the file named Default from directory. Typically, the /etc/X11/gdm/:0 script sets the background to a solid color and displays a logo. The gdm program runs this script as root and waits until the commands finish.
- 2. The gdm program runs /usr/bin/dgreet program, which displays a login box containing fields in which the user can enter their name and password.
- 3. After a user enters a name and password and presses Enter, gdm verifies the password and tries to execute the startup script /etc/X11/gdm/PreSession/DisplayName, where DisplayName is :0 for the first display. If it is not found, gdm executes /etc/X11/gdm/PreSession/Default, if it exists.
- 4. The gdm program runs the session from /etc/X11/gdm/Sessions directory. The exact script that gdm runs depends on the session the user selects in the login menu. For a KDE session, xdm/Xsession script with the argument looks for another script, named .xsession, in the user's home directory and executes that, if exists (img/d9230b719dc0efd80851f363d8c6f571_431_1.png).
- 5. From this point, the user can interact with the system through the X display and through the window manager (started by the gnome-session program).
- 6. When you start the GNOME session (by selecting Log Out from the Main Menu), gdm attempts to run /etc/X11/gdm/PostSession/DisplayName, where DisplayName is :0 for the first display. If file does not exist, gdm executes /etc/X11/gdm/PostSession/Default, if it exists.

Although this brief description of gdm does not show all the details, gdm is what provides the login and takes care of starting the GNOME session. Like other X programs, gdm is highly configurable. For example, the names of the script files in the preceding list are the typical ones, but you can specify other names through the file named gdm.conf, which by default, also resides in the /etc/X11/gdm directory.

# Taking Stock of Fedora Core Configuration Files

Fedora Core includes a host of configuration files. All these files share text files that you can edit with any editor. To edit these configuration files, you must log in as root. I don't discuss the files individually, but I show a selection of the configuration files in Table 1-3, with a brief description of each. This listing gives you an idea of what types of configuration files a system administrator has to work with. In many cases, Fedora Core includes GUI utility programs to set up these configuration files.

### Table 1-3 Some Fedora Core Configuration Files
| Configuration File | Description |
| --- | --- |
| /boot/System.map | Map of the Linux kernel (maps kernel addresses to names of functions and variables) |
| /boot/vmlinuz | The Linux kernel (the operating system's core) |
| /etc/at.allow | Usernames of users allowed to use the at to schedule jobs for later execution |
| /etc/at.deny | Usernames of users forbidden to use the at command |
| /etc/bashrc | Systemwide functions and aliases for the BASH shell |
| /etc/cups/cupsd.conf | Printer configuration file for the Common UNIX Printing System (CUPS) scheduler |
| /etc/fonts | Directory with font files |
| /etc/fstab | Information about file systems available for mounting |
| /etc/group | Information about groups |
| /etc/grub.conf | Configuration for the Grand Unified Bootloader (GRUB) — the default boot loader in Fedora Core (this is a symbolic link to /boot/grub/grub.conf) |
| /etc/hosts | List of IP numbers and their corresponding hostnames |
| /etc/hosts.allow | Hosts allowed to access Internet services on this system |
| /etc/hosts.deny | Hosts forbidden to access Internet services on this system |
| /etc/httpd/httpd.conf | Configuration file for the Apache Web server |
| /etc/init.d | Directory with scripts to start and stop many servers |
| /etc/initab | Configuration file used by the init process that starts all the other processes |
| /etc/issue | File containing a message to be printed before displaying the text-mode login prompt (usually the Fedora Core version number) |
| /etc/lilo.conf | The configuration for the Linux LILO — one of the loaders that load the operating system from disk (present only if you use the LILO boot loader) |
| /etc/login.defs | Default information for creating user accounts, used by the useradd command |
| /etc/modprobe.conf | Configuration file with directives for loading kernel modules (for example, Ethernet and sound drivers) |
| /etc/mtab | Information about currently mounted file systems |


when used this way is read in the root user's environment. As a result, you may type a command that you know is available and get the message “command not found.” To fix this problem, you can use the su command with the dash (-) option instead, as follows:

```
$ su -
Password: ********
#
```

You still need to type the password, but after you do that, everything that normally happens at login for the root user will happen after the su command is completed. Your current directory will be root’s home directory (probably /root, and think that the root user’s PATH variable will be used. If you became the root user by just typing su, rather than su -, you would not have changed directories or the environment of the current login session.

> TIP: When you become super user during someone else’s session, a common mistake is to leave files or directories in the user’s directories that are owned by root. If you do this, be sure to use the chown or chmod command to make the files and directories you modify open to the user that you want to own them. Otherwise, you will probably get a phone call in a short time, asking you to come back and fix it.

You can also use the su command to become another user than root. For example, to have the permissions of a user named chum, you could type the following:

```
$ su - chum
```

Even if you were root user before you typed this command, you would only have the permission to open files and run programs that are available to chum. As root user, however, after you type the su command to become another user, you don’t need a password to continue. If you type that command as a regular user, you must type the new user’s password.

When you are finished using super user permissions, return to the previous shell by exiting the current shell. Do this by pressing Ctrl+D or by typing exit. If you are the administrator for a computer that is accessible to multiple users, don’t leave a root shell open on someone else’s screen (unless you want to let that person do anything they like to the computer!).

When you run GUI tools as a regular user, you are usually prompted for the root password (as described the section “Using graphical administration tools” later in this chapter). If a GUI tool fails and doesn’t prompt you for a password, refer to the “Becoming Super User in X” sidebar.

## Learning about Administrative GUI Tools, Commands, Configuration Files, and Log Files

Fedora and Red Hat Linux systems have advanced enough in recent releases that you can now do most system administration from your desktop GUI, bypassing the shell altogether. Whether you administer Fedora from the GUI or from a shell, however, underlying your activities are many administrative commands, configuration files, and log files.

### Becoming Super User in X

There may be times when an X GUI is running on Linux as a non-root user and you want to run a graphical administration program. In most cases, the GUI administration program will simply prompt you for the root password to continue. However, if the program fails, saying that you don't have permission to run the command, here is what you can do:

First, open a Terminal window on the X desktop.

Then, open permission to the X window display to everyone on the local computer (this is just a temporary measure) by typing:

```
$ xhost +localhost
```

Type the following and enter the root password when prompted, to become super user:

```
$ su -
Password: ******
#
```

Next, type the following to see the current display value:

```
# echo $DISPLAY
```

If the value is something like :0 or 0:0, any X command you run from that shell will appear on the console terminal for the computer. If you are at the console and that's what you see, then you can skip the next step. If you see no value (which is quite possible) or the wrong value, you must set the DISPLAY variable.

Type the following (assuming you are using a bash or sh shell):

```
# export DISPLAY=:0
```

At this point, you can run any administrative X command (such as neat or system-config-packages) and have it appear on your X desktop. If you are running an administrative command from a remote computer and you want it to appear on your local desktop, you can set the DISPLAY to host:0, where host is replaced by the name of your computer.

When you are done, be sure to exit the application you are running. Then restore the security of your X desktop by typing the following:

```
$ xhost -
```

Understanding where GUI tools, commands, and files are located and how they are used will help you effectively maintain your Fedora system. Although most administrative features are intended for the root user, other administrative users (described later in this section) have limited administrative capabilities.

## Using graphical administration tools

The trend over the past few versions of Fedora and other Red Hat Linux distributions has been to steer clear of the massive administrative interfaces (such as linuxconf and Webmin) and instead to offer graphical windows that perform individual administrative tasks. Instead of sharing one monolithic interface, they share common menus. Individual graphical windows for configuring a network, adding users, or setting up printers can be launched from that menu.

> NOTE: In Fedora Core 1 and previous versions of Red Hat Linux, the GUI administration tools all began with redhat-, such as redhat-config-network and redhat-logviewer. Starting with Fedora Core 2, those names have all changed to system-, resulting in names like system-config-network and system-logviewer.

To administer your Fedora system through the GNOME or KDE desktops, Red Hat, Inc. has provided a common menu (Red Hat calls it the Main Menu; I refer to it as the red hat menu). In GNOME, click the red hat; in KDE, click the K icon in the lower-left corner of the desktop.

Because these administrative tasks require root permission, if you are logged in as a regular user you must enter the root password before the GUI application’s window opens. For example, if you launch the System Logs window (System Logs → System Logs) from the GNOME menu as a regular user, you see the pop-up window shown in Figure 10-1.

![](img/b22364e57409c2481ba806e4e6b9309c_386_0.png)

Figure 10-1: Enter the root password to open system administration windows from a regular user’s GUI.

After you have entered the root password, most of the system configuration tools will open without requiring you to retype the password during this login session. Look for a “keys” icon in the lower right corner of the panel, indicating that you have root authorization. Click the keys to open a pop-up window that lets you remove authorization. Otherwise, authorization goes away when you close the GUI window.

> NOTE: As you configure different features on your Fedora or Red Hat Linux system, you are asked to launch different individual graphical windows. In general, if you have a choice of tools for configuring a server or adding a feature, I recommend that you use the tool provided with your distribution. That’s because the Red Hat GUI tools more often integrate closely with the way Fedora and Red Hat systems store and manage their configuration information.

The following list describes many of the GUI-based windows you can use to administer your Fedora or Red Hat Linux system. Start these windows from the System Settings or System Tools submenus on your red hat menu:

- **Server Settings** — This submenu accesses the following server configuration windows:
  - **Domain Name System** — Create and configure zones if your computer is acting as a DNS server.
  - **HTTP** — Configure your computer as an Apache Web server.
  - **NFS** — Set up directories from your system to be shared with other computers on your network using the NFS service.
  - **Samba** — Configure Windows (SMB) file sharing. (To configure other Samba features, you can use the SWAT window. SWAT is described in Chapter 18.)
  - **Services** — Display and change which services are running on your Fedora system at different run levels.
- **Add/Remove Applications** — Manage software packages in the Fedora distribution.
- **Authentication** — Change how users are authenticated on your system. Usually, Shadow Passwords and MD5 Passwords are selected. However, if your network supports LDAP, Kerberos, SMB, NIS, or Hesiod authentication types, you can select to use any of those authentication types.
- **Date & Time** — Set the date and time or choose to have an NTP server keep system time in sync. Figure 10-2 shows the Date/Time Properties window.
- **Disk Management** — Mount and format removable media, such as CDs and floppy disks.
- **Display** — Change the settings for your X desktop, including color depth and resolution for your display. You can also choose settings for your video card and monitor.
- **Hardware Browser** — View information about your computer’s hardware.
- **Internet Configuration Wizard** — Create initial configurations for connecting to the Internet via Ethernet, ISDN, modem, and other types of network equipment.
- **Keyboard** — Choose the type of keyboard you are using, based on language.
- **Kickstart** — Create a Kickstart configuration file that can be used to install multiple Fedora systems without user intervention.
- **Language** — Select the default language used for the system.

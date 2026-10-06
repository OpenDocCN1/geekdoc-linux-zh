
# Chapter 4 ♦ Learning Basic Administration

| File | Description |
|---|---|
| termcap | Lists definitions for character terminals, so that character-based applications know what features are supported by a given terminal. Graphical terminals and applications have made this file obsolete to most people (Termcap was the BSD UNIX way of storing terminal information; UNIX V used definitions in `/usr/share/terminfo` files). |
| inetd.conf | Contains simple configuration information used by the inetd daemon process. This file mostly points to the `/etc/xinetd.d` directory for individual services. (Some systems use `inetd.conf` file and inetd daemon instead). |

Another directory, `/etc/X11`, includes subdirectories that contain system-wide configuration files for X and different window managers for Linux. xorg.conf file (which makes your computer and monitor usable with X) and configuration directories include files used by xdm and xinit to start X are.

Directories relating to window managers contain files that include the default users get if user starts one of these window managers on your system. Window managers that may have system-wide configuration files in these include GNOME (gdm) and Twm (twm).

> Some files and directories in `/etc/X11` are linked to locations in the `/usr/X11R6` directory.

# Administrative Log Files

One of the things Linux does is keep track of itself. This is a good thing, when you consider how much is going on in a complex operating system. Sometimes you are trying to get a new facility working and it fails giving you the fogliest reason why. Other times you want to monitor your system to see if people are accessing your computer illegally. In any of those cases, you can use log files to track down the problem.

The main utilities for logging error and debugging messages for Linux are the syslog and klog daemons. General system logging is done by syslog. Logging that is specific to kernel activity is done by klog. Logging is done according to information in the `/etc/syslog.conf` file. Messages are typically directed to log files that are in the `/var/log` directory. Here are a few common log files:

- boot.log—Contains boot messages about services as they start up.
- messages—Contains many informational messages about the system.
- secure—Contains security-related messages, such as log activity.
- XFree86.0.log—Depending on which X or Xorg.0.log you are using, contains messages about your video card, mouse, and monitor configuration.

If you are using Red Hat Linux system, the System Logs utility is a good way to step through your system's log files. From the red hat menu, select Applications-> System Logs. You can not only view boot, kernel, mail, security, and other system logs, but you can also use the filter box to search for particular terms (such as a model number of a piece of hardware that's not working).

On SUSE systems, you can view log files from YaST. For example, select Miscellaneous and then choose View System Log or Start-Up Log to view the messages or boot.msg files, respectively.

# Using sudo and Other Administrative Logins

You don't hear much about administrative logins (besides root) being used with Linux. It was a common practice in UNIX systems to have several different administrative logins that allowed administrative tasks to be split among users. For example, a person sitting near a printer could have lp permissions to move jobs to another printer if he knew a printer wasn't working.

In any case, administrative logins are available with Linux, so you may want to look into using them. Here are some examples:

- **lp**—Can control printing features. Having a separate lp allows someone other than the superuser to do such things as move or remove logs and print spool files. The home directory for it is /var/spool/lpd.
- **mail**—Can use with administrative email features. The mail group, for many Linux systems, has group permissions to use mail files in /var/spool/mail (which is also the mail user's home directory).
- **uccp**—User owns various u commands (once used as the primary method for dial-up serial communications) as well as log files in /var/log/uccp, spool files in /var/spool, administrative commands (such as uuchk, uucico, uconv, and uucqt) in /usr/sbin. The home directory for uccp is /var/spool/uccp.
- **news**—Could do administration of Internet news services, depending on how you set permission for /var/spool/news and other news-related resources. The home directory for news is /etc/news.

One way to give or limited root privileges to nonroot user is to use the sudo facility, which simply entails adding the user to /etc/sudoers and defining what privilege you want that to have. Then the user can run any command or she is privileged to use by preceding that command with the sudo command.

Here's an example of how to use the sudo facility to cause any users that are added to the wheel group to have full root privileges:

1. As the root user, edit the /etc/sudoers file by running the visudo command:
```bash
/usr/sbin/visudo
```
By default, the file opens in vi, unless your EDITOR variable has been set to some other editor acceptable to visudo (for example, export EDITOR=edit /etc/sudoers file). The reason for using visudo is that the command locks the file and does some basic sanity checking of the file to ensure it has been edited correctly.

> If you are stuck here, refer to the vi tutorial in Chapter 2 for information on using the vi editor.

2. Uncomment the following line to allow users in the wheel group to have full root privileges on the computer:
```bash
%wheel ALL=(ALL) ALL
```
This line causes users in the wheel group to provide a password (their own password, not the root password) in order to use administrative commands. To allow users in the wheel group to have privilege without password, uncomment the following line:
```bash
%wheel ALL=(ALL) NOPASSWD: ALL
```

3. Save the changes to the /etc/sudoers file (in vi).

4. Still as root user, open the /etc/group file in any text editor and add the wheel line you want to have root privilege, if you were to add the users mary and jake to the wheel group, the line would appear as follows:
```text
wheel:x:10:root,mary,jake
```
Now users mary and jake can run the sudo command to run commands, or parts of commands, that are normally restricted to the root user. The following is an example of a session by the jake user after he has assigned sudo privileges:

```
[jake]$ sudo mount /mnt/win
```
We trust you have received the usual lecture from the local System Administrator. It usually boils down to these two things:

```
#1) Respect the privacy of others.
#2) Think before you type.
```
```
Password: ********
[jake]$ mount /mnt/win
mount: only root can mount /dev/hda /mnt/win
[jake]$ sudo mount /mnt/win
[jake]$
```

In this session, the user jake runs the sudo command to unmount the /mnt/win file system (using the mount command). He is given a warning and asked to provide his password (this is jake's password, not the root password).

Even after jake has given the password, he must still use the sudo command to run subsequent administrative commands as root (the mount fails, but sudo succeeds). Notice that he is not prompted for a password for the second sudo command. That's because after entering his password successfully, he can enter as many sudo commands as he wants for 5 minutes without having to enter again. (You can change the timeout from 5 minutes to however long you want by setting passwd_timeout value in theetc/sudoers file.)

The preceding example grants a single-or-nothing privilege to everyone you in the wheel group. However, the /etc/sudoers file gives you an incredible amount of flexibility in permitting individual users and groups to use individual applications or groups of applications. Refer to the sudoers and sudo man pages for information about how to tune your sudo facility.

# Administering Your Linux System

Your system administrator duties don't end after you have installed Linux. Multiple people are using your Linux system, you, as administrator, must give each person his own login account. You use useradd and related commands to add, modify, and delete user accounts.

Configuring hardware is also on your duty list. When you add hardware to your Linux computer, hardware is detected and configured automatically. In some cases, the hardware may not have been set up properly and you will use commands as ismod, insmod, and rmod to configure the right modules.

> A device driver is the code permanently built into the kernel to allow application programs to talk to a particular piece of hardware. A module is like a driver, but it is loaded on demand. The "Configuring Hardware" section later in this chapter includes information about how to configure modules.

Managing files and disk space is your responsibility, you must keep track of the disk space being consumed, especially if your Linux system is shared by multiple users. At some point, you may need to add a hard disk or track what is eating your disk space (use commands such as find to do this).

Your duties also include monitoring system performance. You may have a runaway process on your system or you may be experiencing slow performance. Tools that come with Linux can help you determine how much of your CPU and memory are consuming.

These tasks are explored in the rest of this chapter.

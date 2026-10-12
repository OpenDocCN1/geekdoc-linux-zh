
The `/etc/X11/gdm/gdm.conf` file has many comment lines—these lines begin with a hash mark (#). Labels within square brackets ([...]) identify various sections of the file. The different sections in the configuration file control different aspects of the graphical login screen as well as the tasks the user can perform from that screen.

You see the term greeter used often in the display manager configuration file. Greeter refers to the login screen—the user interface through which the display manager prompts the user to log in to the system.

![](img/9f89727199836b0f871f1745838aa8b2_431_0.png)

Edit the `Welcome=` line in `/etc/X11/gdm/gdm.conf` to change the welcome message on the graphical login screen. The default message says welcome to the hostname, which can be somewhat cryptic. You can edit that line and change the message to something more meaningful with the syntax `Welcome=Welcome to ABC Corp.`

**GNOME session startup under gdm**

For the default configuration after a typical Fedora Core installation with the GNOME desktop, `gdm` manages the login session as follows:

- 1. The `gdm` program starts the X server and looks for a script named after the local display’s name (for the first display, the filename is `:0` in the `/etc/X11/gdm/Init` directory. If it does not find that file, `gdm` executes the file named `Default` from that directory. Typically, the `/etc/X11/gdm/Init/:0` script sets the background to a solid color and displays a logo. The `gdm` program runs this script as `root` and waits until the commands finish.
- 2. The `gdm` program runs the `/usr/bin/gdmgreeter` program, which displays a dialog box that contains fields in which the user can enter a name and a password.
- 3. After a user enters a name and password and presses Enter, `gdm` verifies the password and tries to execute the startup script `/etc/X11/gdm/PreSession/DisplayName`, where `DisplayName` is `:0` for the first display. If that file is not found, `gdm` executes the `/etc/X11/gdm/PreSession/Default` script, if it exists.
- 4. The `gdm` program runs the session script from the `/etc/X11/gdm/Sessions` directory. The exact script that `gdm` runs depends on the session the user selects in the Sessions menu in the `gdm` greeter display. For a GNOME session, `gdm` runs the `/etc/X11/xdm/XSession` script with `gnome` as the argument. For a KDE session, `gdm` runs the `/etc/X11/xdm/XSession` script with `kde` as the argument. The `/etc/X11/xdm/Xsession` looks for another script file, named `.xsession`, in the user’s home directory and executes that script, if it exists. Next, it looks for the `.xclients` script file in the user’s home directory and executes that file, if it exists. Otherwise, `xsession` executes the `/etc/X11/xinit/xclients` script. When you follow through these scripts, you find that the `xclients` script executes the `/usr/bin/gnome-session` program if the `/etc/sysconfig/desktop` file contains the line `DESKTOP="GNOME"`. The `gnome-session` program then starts the GNOME session (which includes a set of applications and a window manager). Initially, `gnome-session` uses the session file `/usr/share/gnome/default.session` (a text file) to start the applications and the window manager. Later, the GNOME session is re-stored to the values saved in a file in the `~/.metacity/sessions` directory (this path refers to a subdirectory in your home directory). The default session file runs a script named `/usr/bin/gnome-wm`, which, in turn, starts an appropriate window manager. The default window manager is `metacity`, but you can specify a different window manager by defining the `WINDOW_MANAGER` environment value to the name of a window manager you want.
- 5. From this point on, the user can interact with the system through the X display and through the window manager (started by the `gnome-session` program).
- 6. When the user ends the GNOME session (by selecting Log Out from the Main Menu), `gdm` attempts to run the script `/etc/X11/gdm/PostSession/DisplayName`, where `DisplayName` is `:0` for the first display. If that file does not exist, `gdm` executes the `/etc/X11/gdm/PostSession/Default` script, if it exists.

Although this brief description of `gdm` does not show you all the details, `gdm` is what provides the GUI login and takes care of starting a GNOME session. Like many other X programs, `gdm` is highly configurable. For example, the names of the script files in the preceding list are the typical ones, but you can specify other names through the file named `gdm.conf`, which, by default, also resides in the `/etc/X11/gdm` directory.

## Taking Stock of Fedora Core System Configuration Files

Fedora Core includes a host of configuration files. All these files share text files that you can edit with any text editor. To edit these configuration files, you must log in as `root`. I don’t discuss the files individually, but I show a selection of the configuration files in Table 1-3, along with a brief description of each. This listing gives you an idea of what types of configuration files a system administrator has to work with. In many cases, Fedora Core includes GUI utility programs to set up many of these configuration files.

### Table 1-3 Some Fedora Core Configuration Files

| Configuration File | Description |
|---|---|
| /boot/system.map | Map of the Linux kernel (maps kernel addresses into names of functions and variables) |
| /boot/vmlinuz | The Linux kernel (the operating system’s core) |
| /etc/at.allow | Usernames of users allowed to use the at command to schedule jobs for later execution |
| /etc/at.deny | Usernames of users forbidden to use the at command |
| /etc/bashrc | Systemwide functions and aliases for the BASH shell |
| /etc/cups/cpsh.conf | Printer configuration file for the Common UNIX Printing System (CUPS) scheduler |
| /etc/fonts | Directory with font configuration files |
| /etc/fstab | Information about file systems available for mounting |
| /etc/group | Information about groups |
| /etc/grub.conf | The configuration for the Grand Unified Bootloader (GRUB) — the default boot loader in Fedora Core (this file is a symbolic link to /boot/grub/grub.conf) |
| /etc/hosts | List of IP numbers and their corresponding hostnames |
| /etc/hosts.allow | Hosts allowed to access Internet services on this system |
| /etc/hosts.deny | Hosts forbidden to access Internet services on this system |
| /etc/httpd/conf/httpd.conf | Configuration file for the Apache Web server conf |
| /etc/init.d | Directory with scripts to start and stop many servers |
| /etc/inittab | Configuration file used by the init process that starts all the other processes |
| /etc/issue | File containing a message to be printed before displaying the text-mode login prompt (usually the Fedora Core version number) |
| /etc/lilo.conf | The configuration for the Linux Loader (LILO)—one of the boot loaders that can load the operating system from disk (present only if you use the LILO boot loader) |
| /etc/login.defs | Default information for creating user accounts, used by the useradd command |
| /etc/modprobe.conf | Configuration file with directives for loading kernel modules (for example, Ethernet and sound drivers) |
| /etc/mstab | Information about currently mounted file systems |
| /etc/passwd | Information about all user accounts (actual passwords are stored in `/etc/shadow`) |
| /etc/profile | Systemwide environment and startup file for the BASH shell |
| /etc/rc.d | Directory that holds startup and shutdown scripts for the Fedora Core system |
| /etc/rc.d/rc.sysinit | Fedora Core initialization script |
| /etc/shadow | Secure file with encrypted passwords for all user accounts (can be read only by root) |
| /etc/shells | List of all the shells on the system that the user can use |
| /etc/skel | Directory that holds initial versions of files such as `.bash_profile` that copy to a new user’s home directory |
| /etc/sysconfig | Fedora Core configuration files |
| /etc/sysctl.conf | Configuration file with kernel parameters that are read in and set by `sysctl` at system startup |
| /etc/termcap | Database of terminal capabilities and options |
| /etc/udev | Directory containing configuration files for `udev` — the program that provides the ability to dynamically name hot-pluggable devices and create device files in the `/dev` directory |
| /etc/X11/xorg.conf | Configuration file for X.org X11 — the X Window System |
| /etc/X11/gdm | Directory with configuration files for the GNOME display manager (gdm) |
| /etc/xinetd.conf | Configuration for the `xinetd` daemon that starts a number of Internet services on demand |
| /etc/yum.conf | Configuration for the `yum` package updater and installer |
| /var/log/cron | Log file with messages from the `cron` process that runs scheduled jobs |
| /var/log/httpd/access_log | Web-server access log |
| /var/log/httpd/error_log | Web-server error log |
| /var/log/messages | System log |

## Monitoring System Performance

When you’re the system administrator, you must keep an eye on how well your Fedora Core system is performing. You can monitor the overall performance of your system by looking at information such as


## Starting System Services
Starting crond: [ OK ]  
Starting xfs: [ OK ]  
Starting anacron: [ OK ]  
Starting atd: [ OK ]

However, these messages are hidden by the graphical boot screen by default; to see these messages, you must click **Show Details** on the graphical boot screen. To view them afterward, recall from Chapter 7, “Advanced Installation,” that you can view the contents of the `/var/log/boot.log` and `/var/log/messages` log files.

The remainder of the `/etc/inittab` file loads optional components and allows for login programs to run on terminals. For terminal logins, the `mingetty` program is started on `tty1` through `tty6` and restarted (`respawn`) continuously to allow for login after login. In addition, `gdm` is started only upon entering runlevel 5 from the last entry in `/etc/inittab`.

After the entries in `/etc/inittab` have been executed, the `/etc/rc.d/rc.local` file is executed to perform tasks that must occur after system startup. The entire Linux initialization process is summarized in Figure 9-9.

![](img/09bf13b782f71165e17bb3839040c96a_368_0.png)  
*FIGURE 9-9 The Linux initialization process*

## Configuring Daemon Startup
Recall from the preceding section that most daemons are started by the `init` daemon from symbolic links in the `/etc/rc.d/` directories depending on the runlevel entered. Most of these links point to the appropriate daemon executable file in the `/etc/rc.d/init.d/` directory. A partial listing of the `/etc/rc.d/rc5.d` directory demonstrates this:

```bash
[root@server1 root]# ls -l /etc/rc.d/rc5.d | head
total 0
lrwxrwxrwx 1 root root 13 Jun 11 08:46 K01yum -> ../init.d/yum
lrwxrwxrwx 1 root root 14 Jun 11 10:17 K05innd -> ../init.d/innd
lrwxrwxrwx 1 root root 19 Jun 11 08:45 K05saslauthd -> ../init.d/saslauthd
lrwxrwxrwx 1 root root 19 Jun 11 08:46 K10dc_server -> ../init.d/dc_server
lrwxrwxrwx 1 root root 16 Jun 11 08:45 K10psacct -> ../init.d/psacct
lrwxrwxrwx 1 root root 17 Jun 11 10:16 K10radiusd -> ../init.d/radiusd
lrwxrwxrwx 1 root root 19 Jun 11 08:46 K12dc_client -> ../init.d/dc_client
lrwxrwxrwx 1 root root 17 Jun 11 10:15 K12mailman -> ../init.d/mailman
lrwxrwxrwx 1 root root 16 Jun 11 10:18 K12mysql -> ../init.d/mysql
[root@server1 root]# 
```

In addition, most daemons accept the arguments `start`, `stop`, and `restart`. Thus, to manipulate daemons after system startup, you can execute them directly from the `/etc/rc.d/init.d` directory, as shown next with the `xinetd` daemon:

```bash
[root@server1 root]# /etc/rc.d/init.d/xinetd restart
Stopping xinetd:                [ OK ]
Starting xinetd:                [ OK ]
[root@server1 root]# 
```

![](img/09bf13b782f71165e17bb3839040c96a_369_0.png)

> **NOTE**  
> The `/etc/init.d` directory is symbolically linked to the `/etc/rc.d/init.d` directory; thus, the `/etc/init.d/xinetd restart` command would perform the same function as the command used in the preceding example.

Because most daemon executable files are centrally stored in the `/etc/rc.d/init.d` directory, if you want to add a daemon that is automatically started by the `init` daemon upon entering a certain runlevel at system startup, you can add the executable file for the daemon to this directory and create the appropriate links in each of the `/etc/rc.d/rc*.d` directories to start or kill the daemon upon entering certain runlevels.

Thus, to configure the `init` daemon to automatically start an executable daemon file called `test-daemon` when entering runlevels 2, 3, and 5, you can perform the following commands:

```bash
[root@server1 root]# cp testdaemon /etc/rc.d/init.d
[root@server1 root]# cd /etc/rc.d/init.d
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc2.d/S99testdaemon
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc3.d/S99testdaemon
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc5.d/S99testdaemon
[root@server1 root]# 
```

Similarly, to configure the `init` daemon to automatically kill `testdaemon` when entering run-level 0, 1, and 6, you can execute the following commands:

```bash
[root@server1 root]# cd /etc/rc.d/init.d
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc0.d/K01testdaemon
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc1.d/K01testdaemon
[root@server1 root]# ln -s testdaemon /etc/rc.d/rc6.d/K01testdaemon
[root@server1 root]# 
```

To see whether the daemon loaded successfully at boot time, simply view the contents of the `/var/log/messages` file after the system has fully initialized, as shown next:

```bash
[root@server1 root]# grep testdaemon /var/log/messages
Jun 15 12:44:34 server1 testdaemon: testdaemon startup succeeded
[root@server1 root]# 
```

For ease of administration, Red Hat Fedora places a large number of files that start with `K` in most `/etc/rc.d/rc*.d` directories even though the daemons represented by those files are not likely started. This allows a user to rename the file such that it starts with `S` to start the daemon upon entering that runlevel. Alternatively, you can use the `ntsysv` utility to modify the file entries in the `/etc/rc.d/rc*.d` directories.

If you type `ntsysv --level 5` to modify the daemons that will be started in runlevel 5, the screen depicted in Figure 9-10 is displayed.

![](img/09bf13b782f71165e17bb3839040c96a_370_0.png)

## The X Windows System
Until this section, focus has been placed on performing tasks using a BASH shell command-line interface obtained after logging in to a character terminal. Although the command-line interface is the most common among administrators, graphical user interfaces (GUIs) can be used to simplify some administrative tasks. In addition, Linux users typically use graphical interfaces for running user programs; thus, it is important to possess a good understanding of the components that the Linux GUI comprises, as well as how to start, stop, and configure them.

### Linux GUI Components
The Linux graphical user interface (GUI) was designed to function in the same manner regardless of the video hardware on the computer system. As a result, it is composed of many components, which work separately from the video hardware (video adapter card and monitor). These components are illustrated in Figure 9-11.

![](img/09bf13b782f71165e17bb3839040c96a_371_0.png)

**FIGURE 9-11** _Components of the Linux GUI_

A large part of a typical Linux installation comprises all of the components listed in Figure 9-11. A typical installation of Red Hat Fedora Linux usually uses 2–4 GB of data on the hard disk for the GUI and related programs.

### X Windows
The core component of the GUI in Linux is **X Windows**. X Windows provides the ability to draw graphical images in windows that are displayed on a terminal screen. The programs that tell X Windows how to draw the graphics and display the results are known as **X clients**. X clients need not run on the same computer as X Windows; you can use X Windows on one computer to send graphical images to an X client on an entirely different computer by changing the `DISPLAY` environment variable discussed in Chapter 8, “Working with the BASH Shell.” Because of this, X Windows is sometimes referred to as the server component of X Windows, or simply the **X server**.

X Windows was jointly developed by Digital Equipment Corporation (DEC) and the Massachusetts Institute of Technology (MIT) in 1984. Then, it was code-named Project Athena and was released in 1985 as X Windows in hopes that a new name would be found to replace the X. Shortly thereafter, X Windows was sought by many UNIX vendors and by 1988, MIT released version 11 release 2 of X Windows (X11R2). Since 1988, X Windows has been maintained by The Open Group, which released version 11 release 6 of X Windows (X11R6) in 1995. Since 2004, X Windows has been maintained as Open Source Software by the X.org Foundation.

![](img/09bf13b782f71165e17bb3839040c96a_372_0.png)

> **NOTES**  
> To find out more about X Windows, visit the X.org Foundation on the Internet at <http://www.x.org>.

Until recently, X Windows was governed by a separate license than the GPL, which restricted the usage of X Windows and its source code. As a result, open source developers created an open source version of X Windows in the 1990s. This freely available version of X Windows is used in many Linux distributions and is called **XFree86** because it was originally intended for the Intel x86 platform.

![](img/09bf13b782f71165e17bb3839040c96a_372_1.png)

> **NOTE**  
> To find out more about XFree86, visit the XFree86 Project on the Internet at <http://www.xfree86.org>.

Today, Linux distributions offer either X Windows or the XFree86 implementation of X Windows because they are both Open Source Software. Red Hat Fedora Core 2 uses X Windows instead of XFree86.

### Window Managers and Desktop Environments
Although X Windows performs most of the graphical functions in a GUI, there also exists a **Window Manager** that modifies the look and feel of X Windows. Thus, to change the appearance and behavior of X Windows, you can simply change the Window Manager used with X Windows. Optionally, you can use a **desktop environment** in addition to a Window Manager. Desktop environments come with a full set of GUI tools designed to be packaged together, including Web browsers, file managers, and drawing programs. Desktop environments also provide development “toolkits” that allow software to be created more rapidly in much the same manner as other environments.

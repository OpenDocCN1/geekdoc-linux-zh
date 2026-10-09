
Following is the job definition file for the service that starts and monitors the getty process (page 448) on tty1:

```bash
$ cat /etc/init/tty1.conf
# tty1 - getty
#
# This service maintains a getty on tty1 from the point the system is
# started until it is shut down again.

start on stopped rc RUNLEVEL=[2345]
stop on runlevel [!2345]

respawn
exec /sbin/getty -8 38400 tty1
```

The event in the start on stanza is named **stopped** (see the **stopped man** page). This stanza starts the tty1 service when the **rc** task is stopped with **RUNLEVEL** equal to 2, 3, 4, or 5. Because the **rc** task is stopped as the system finishes entering each of these runlevels, the tty1 service starts when the system enters any of these runlevels.

The event in the **stop on** stanza is named **runlevel**. This stanza stops the tty1 service when a **runlevel** event is emitted with an argument other than 2, 3, 4, or 5—that is, when the system enters recovery mode, is shut down, or is rebooted.

The **respawn** keyword tells init to restart the tty1 service if it terminates. The **exec** stanza runs a getty process with no party (-8) on tty1 at 38,400 baud. In the next example, the **initctl** utility reports that the **tty1** service has started and is running as process 1061; **ps** reports on the process:

```bash
$ status tty1
tty1 start/running, process 1061
$ ps -ef | grep 1061
root     1061   1  0 12:26 tty1    00:00:00 /sbin/getty -8 38400 tty1
```

See page 451 for a discussion of the **control-alt-delete** task, which you can use to bring the system down.

Under SysVinit, the **initdefault** entry in the **/etc/inittab** file tells init which runlevel (page 443) to bring the system to when it comes up. Ubuntu does not include an inittab file; instead, by default, the Upstart init daemon (using the **rc-sysinit** task) boots the system to multiuser mode (runlevel 2). If you want the system to boot to a different runlevel, modify the following line in the rc-sysinit.conf file:

```bash
$ cat /etc/init/rc-sysinit.conf
...
env DEFAULT_RUNLEVEL=2
...
```

### Do not set the system to boot to runlevel 0 or 6

Never set the system to boot to runlevel 0 or 6, as it will not come up properly. To boot to multiuser mode (runlevel 2), set **DEFAULT_RUNLEVEL** to 2. To boot to recovery mode, set **DEFAULT_RUNLEVEL** to 5.

Changing the value of `DEFAULT_RUNLEVEL` from 2 to 5 causes the system to boot to recovery mode (runlevel 5; see the caution on page 444). When the system comes up in recovery mode, if the **root** account on the system is unlocked (page 431), `init` requests the **root** password before displaying the **root** prompt. Otherwise, it displays the **root** prompt without requesting a password.

## SysVinit (rc) Scripts: Start and Stop System Services

- **rc scripts**: The init (initialization) scripts, also called **rc** (run command) scripts, are shell scripts located in the `/etc/init.d` directory. They are run via symbolic links in the `/etc/rcn.d` directories, where *n* is the runlevel the system is entering.

> As explained on page 434, Ubuntu emulates runlevels using Upstart to aid migration and provide compatibility with software for other distributions. This section explains how `init` scripts work with (emulated) runlevels to control system services. Many of the scripts in the /etc/rcn.d and /etc/init.d directories described in this section suggest you use the corresponding `initctl` commands in place of the script because the links in these directories having been replaced by job control files in `/etc/init` (page 434).

The `/etc/rcn.d` directories contain scripts whose names begin with K (K19`cupsys`, K20`dhcp`, K74`bluetooth`, and so on) and scripts whose names begin with S (S15`bind9`, S18`is`, S20`exim4`, and so on). When entering a new runlevel, each K (kill) script is executed with an argument of `stop`, and then each S (start) script is executed with an argument of `start`. Each of the K files is run in numerical order. The S files are run in similar fashion. This arrangement allows the person who sets up these files to control which services are stopped and which are started, and in what order, whenever the system enters a given runlevel. Using scripts with **start** and **stop** arguments promotes flexibility because it allows one script to both start and kill a process, depending on which argument it is called with.

To customize system initialization, you can add shell scripts to the `/etc/init.d` directory and place links to these files in the `/etc/rcn.d` directories (although in practice it is best to use `sysv-rc-conf` [discussed next] to create the links).

The following example shows several links to the `cupsys` init script. These links are called to run the `cupsys` init script to start or stop the `cupsys` daemons at various runlevels:

```bash
$ ls -l /etc/rc*/s*cupsys*
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc1.d/K80cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc2.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc3.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc4.d/S50cupsys -> ../init.d/cupsys
lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc5.d/S50cupsys -> ../init.d/cupsys
```

Each link in `/etc/rcn.d` points to a file in `/etc/init.d`. For example, the file `/etc/rc2.d/S50cupsys` is a link to the file named `cupsys` in `/etc/init.d`. (The numbers in the filenames of the links in the `/etc/rcn.d` directories may change from one release of Ubuntu to the next, but the scripts in `/etc/init.d` always have the same names.)

The names of files in the init.d directory are functional. Thus, when you want to turn NFS services on or off, you use the nfs-kernel-server script. Similarly, when you want to turn basic networking services on or off, you run the networking script. The cups script controls the printer daemon. Each script takes an argument of stop or start, depending on what you want to do. Some scripts also take other arguments, such as restart, reload, and status. Run a script without an argument to display a usage message indicating which arguments it accepts.

Following are three examples of calls to init scripts. You may find it easier to use service (discussed next) in place of the pathnames in these commands:

```bash
$ sudo /etc/init.d/nfs-kernel-server stop
$ sudo /etc/init.d/networking start
$ sudo /etc/init.d/networking restart
```

The first example stops all NFS server processes (processes related to serving file-systems over the network). The second example starts all processes related to basic network services. The third example stops and then restarts these same processes.

The /etc/rc.local file is executed after the other init scripts when the system boots. Put commands that customize the system in rc.local. Although you can add any commands you like to rc.local, it is best to run them in the background; that way, if they hang, they will not stop the boot process.

## Service: Configures Services I

Ubuntu provides `service`, a handy utility that can report on or change the status of any of the jobs in /etc/init (page 435) and any of the system services in /etc/init.d (page 440). Ubuntu introduced this utility for compatibility with the Fedora/RHEL `service` utility. In place of the commands described at the end of the previous section, you can give the following commands from any directory:

```bash
$ sudo service nfs-kernel-server stop
$ sudo service networking start
$ sudo service networking restart
```

The command `service --status-all` displays the status of all system services. The next section explores yet another way to configure system services.

## Sysv-rc-conf: Configures Services II

The `sysv-rc-conf` utility (sysv-rc-conf package) makes it easier for a system administrator to maintain the `/etc/init.d` directory hierarchy. This utility can add, remove, and list startup information for system services. You might also want to try the graphical boot-up manager, `bum` (bum package), which this book does not cover.

You can run `sysv-rc-conf` in pseudographical or textual mode. In pseudographical mode, it makes changes to configuration files as you enter the changes and can also start and stop services. For more information on this mode, see the `sysv-rc-conf` man page or run `sysv-rc-conf` without any arguments and give the command `h`. This section discusses using `sysv-rc-conf` in textual mode in which it changes the configuration

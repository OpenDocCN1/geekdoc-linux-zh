
## CHANGING THE CURRENT RUNLEVEL

The systemctl isolate command changes the current runlevel of the system. The following command changes the runlevel to multiuser graphical mode (graphical.target). When the system is rebooted, it will return to the default runlevel as specified by the link at /etc/systemd/system/default.target.

```
# systemctl isolate graphical.target
```

After a moment systemctl shows that, again, both graphical.target and multi-user.target are active:

```
$ systemctl list-units --type=target | egrep 'multi-user|graphical' 
 graphical.target loaded active active Graphical Interface
 multi-user.target loaded active active Multi-User System
```

The preceding examples were run from an ssh login. If you give these commands from a terminal emulator running on the console, the system will log you out each time it changes runlevels.

## CONFIGURING DAEMONS (SERVICES)

Two states are important when you consider a daemon: its current state and its persistent state (the state it will be in after the system is booted). Possible states are running and stopped. When you install a package that includes a daemon, the daemon is stopped and is not set up to start when the system is booted.

The systemctl utility controls the current and persistent states of daemons that run natively under systemd. The service and chkconfig utilities originally controlled daemons that run under SysVinit and were upgraded to control daemons that run under Upstart. Now these utilities have been retrofitted to control daemons that run under systemd, which they do by calling systemctl. You can still use service to control the current state of a daemon and chkconfig to control the persistent state of a daemon.

The next sections describe the systemctl commands that control daemons.

### SETTING THE PERSISTENT STATE OF A DAEMON

The systemctl disable command causes a daemon not to start when the system is booted. This command has no effect on the current state of the daemon. You do not need to specify the .service part of the service name.

```
# systemctl disable atd.service
rm '/etc/systemd/system/multi-user.target.wants/atd.service'
```

The preceding command removes the link that causes systemd to start atd when the system enters multi-user runlevel and, by inheritance, graphical runlevel. See “/etc/systemd/system Hierarchy: Controls Services and the Persistent Runlevel” on page 441 for a discussion of these links.

The following commands each verify that the atd daemon will not start when the system boots. The first command shows no links in the .wants directories for atd.service. The second uses the `systemctl is-enabled` command, which returns disabled.

```
$ ls /etc/systemd/system/\.wants/atd.service
ls: cannot access `/etc/systemd/system/\.wants/atd.service': No such file or directory
$ systemctl is-enabled atd.service
disabled
```

The `systemctl enable` command causes a daemon to start when the system is booted. This command has no effect on the current state of the daemon. The following command creates the link that causes systemd to start atd when the system enters multiuser textual mode and, by inheritance, multiuser graphical mode.

```
# systemctl enable atd.service
ln -s `/usr/lib/systemd/system/atd.service` `/etc/systemd/system/multi-user.target.wants/atd.service`
```

As in the preceding example, the next two commands check whether the daemon will start when the system is booted.

```
$ ls /etc/systemd/system/\.wants/atd.service
/etc/systemd/system/multi-user.target.wants/atd.service
$ systemctl is-enabled atd.service
enabled
```

### CHANGING THE CURRENT STATE OF A DAEMON

The `systemctl stop` command immediately stops a daemon from running. This command has no effect on whether the daemon starts when the system is booted. The following command works on the atd daemon, which is run natively by systemd. It will also work on a daemon systemd controls via a SysVinit script. You do not need to specify the .service part of the service name.

```
# systemctl stop atd.service
```

The preceding command stops the atd daemon and displays no output. The following commands each verify that the atd daemon is not running.

```
$ systemctl status atd.service
atd.service - Job spooling tools
Loaded: loaded (/usr/lib/systemd/system/atd.service; enabled)
Active: inactive (dead) since Wed 2013-07-24 18:03:18 PDT; 53s ago
Main PID: 404 (code=exited, status=0/SUCCESS)
CGroup: name=systemd:/system/atd.service
Jul 24 18:03:18 guava.example.com systemd[1]: Stopping Job spooling tools...
Jul 24 18:03:18 guava.example.com systemd[1]: Stopped Job spooling tools.

$ systemctl is-active atd.service
inactive
```

The `systemctl status` command shows an Active status of *inactive (dead)*. The `systemctl is-active` command displays a status of *inactive*. You can also use `ps -ef | grep atd` to determine whether the daemon is running.

The cups service is managed by systemd. It may be started to run in the background, or activated on demand, or run once for preparation or cleanup purposes.

![](img/243613168ac865b539f12460d966088e_503_0.png)

**Figure 10-1** The Service Configuration window

The `systemctl start` command immediately starts a daemon running. This command has no effect on whether the daemon starts when the system is booted.

```
# systemctl start atd.service
```

The next two commands each show the daemon is running.

```
$ systemctl status atd.service
atd.service - Job spooling tools
    Loaded: loaded (/usr/lib/systemd/system/atd.service; enabled)
    Active: active (running) since Wed 2013-07-24 18:06:55 PDT; 41s ago
  Main PID: 2010 (atd)
   CGroup: name=systemd:/system/atd.service
           ├-2010 /usr/sbin/atd -f

Jul 24 18:06:55 guava.example.com systemd[1]: Started Job spooling tools.

$ systemctl is-active atd.service
active
```

## system-config-services: CONFIGURES SERVICES

The `system-config-services` utility (system-config-services package) displays the Service Configuration window (Figure 10-1). Open this window by giving the command system-config-services from an Enter a Command window (ALT-F2) or a terminal emulator. This utility uses a GUI to provide the functionality of the systemctl start and stop commands (see “Changing the Current State of a Daemon” on page 446) as well as the enable and disable commands (see “Setting the Persistent State of a Daemon” on page 445). It turns system services on and off immediately, and it controls which services are started when the system boots.

The left side of the Service Configuration window displays a scrollable list of services (daemons). Scroll to and highlight the service you want to work with; the right side of the window displays a description of the service. Click the buttons on the toolbar to start (triangle), stop (square), enable (plugged in plug), or disable (unplugged plug) the highlighted service. The Start and Stop buttons turn the service on or off immediately; the Enable and Disable buttons specify whether the service will run the next time the system boots.

### SysVinit (rc) Scripts: Start and Stop System Services

**rc scripts** The SysVinit daemon is driven by init (initialization) scripts. These scripts, also called rc (run command) scripts, are shell scripts located in the *etc/rc.d/init.d* directory. A symbolic link at /etc/init.d points to /etc/rc.d/init.d. The scripts are run via symbolic links in the /etc/rc.d/rcn.d directories, where *n* is the runlevel the system is entering.

> Most of the files in the /etc/rc.d/rcn.d and /etc/rc.d/init.d directories are gone
> Under systemd, Linux uses targets with the names of runlevels to aid migration and provide compatibility with software for other distributions (see Table 10-1). Most of the files in the /etc/rc.d/rcn.d and /etc/rc.d/init.d directories have gone away; they have been replaced by systemd service files.

The /etc/rc.d/rcn.d directories contain scripts whose names begin with K and scripts whose names begin with S. When entering a new runlevel, each K (kill) script is executed with an argument of stop, and then each S (start) script is executed with an argument of start. Each of the K files is run in numerical order. The S files are run in similar fashion. This arrangement allows the person who sets up these files to control which services are stopped and which are started, and in what order, whenever the system enters a given runlevel. Using scripts with start and stop arguments promotes flexibility because it allows one script to both start and kill a process, depending on which argument it is called with.

You can use systemctl (page 445) or system-config-services (previous page) to run SysVinit scripts.

### System Operation

This section covers the basics of how the system functions and can help you make intelligent decisions as a system administrator. It is a guide to bringing a system up and keeping it running day to day.

of the window displays a description of the service. Click the buttons on the toolbar to start (triangle), stop (square), enable (plugged in plug), or disable (unplugged plug) the highlighted service. The Start and Stop buttons turn the service on or off immediately; the Enable and Disable buttons specify whether the service will run the next time the system boots.

# ## SysVinit (rc) Scripts: Start and Stop System Services

**rc scripts** The SysVinit daemon is driven by init (initialization) scripts. These scripts, also called rc (run command) scripts, are shell scripts located in the *etc/rc.d/init.d* directory. A symbolic link at /etc/init.d points to /etc/rc.d/init.d. The scripts are run via symbolic links in the /etc/rc.d/rcn.d directories, where *n* is the runlevel the system is entering.

> Most of the files in the /etc/rc.d/rcn.d and /etc/rc.d/init.d directories are gone
> Under systemd, Linux uses targets with the names of runlevels to aid migration and provide compatibility with software for other distributions (see Table 10-1). Most of the files in the /etc/rc.d/rcn.d and /etc/rc.d/init.d directories have gone away; they have been replaced by systemd service files.

The /etc/rc.d/rcn.d directories contain scripts whose names begin with K and scripts whose names begin with S. When entering a new runlevel, each K (kill) script is executed with an argument of stop, and then each S (start) script is executed with an argument of start. Each of the K files is run in numerical order. The S files are run in similar fashion. This arrangement allows the person who sets up these files to control which services are stopped and which are started, and in what order, whenever the system enters a given runlevel. Using scripts with start and stop arguments promotes flexibility because it allows one script to both start and kill a process, depending on which argument it is called with.

You can use systemctl (page 445) or system-config-services (previous page) to run SysVinit scripts.

# ## System Operation

This section covers the basics of how the system functions and can help you make intelligent decisions as a system administrator. It is a guide to bringing a system up and keeping it running day to day.
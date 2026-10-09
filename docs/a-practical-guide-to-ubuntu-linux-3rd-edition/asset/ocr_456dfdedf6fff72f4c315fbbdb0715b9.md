Changing the value of `DEFAULT_RUNLEVEL` from 2 to 5 causes the system to boot to recovery mode (runlevel 5; see the caution on page 444). When the system comes up in recovery mode, if the **root** account on the system is unlocked (page 431), `init` requests the **root** password before displaying the **root** prompt. Otherwise, it displays the **root** prompt without requesting a password.

# # SysVinit (rc) SCRIPTS: START AND STOP SYSTEM SERVICES

`rc scripts` The init (initialization) scripts, also called **rc** (run command) scripts, are shell scripts located in the `/etc/init.d` directory. They are run via symbolic links in the `/etc/rcn.d` directories, where $n$ is the runlevel the system is entering.

# ## Most of the files in the /etc/rcn.d and /etc/init.d directories will go away

> As explained on page 434, Ubuntu emulates runlevels using Upstart to aid migration and provide compatibility with software for other distributions. This section explains how `init` scripts work with (emulated) runlevels to control system services. Many of the scripts in the /etc/rcn.d and /etc/init.d directories described in this section suggest you use the corresponding `initctl` commands in place of the script because the links in these directories having been replaced by job control files in `/etc/init` (page 434).

The `/etc/rcn.d` directories contain scripts whose names begin with K (K19`cupsys`, K20`dhcp`, K74`bluetooth`, and so on) and scripts whose names begin with S (S15`bind9`, S18`is`, S20`exim4`, and so on). When entering a new runlevel, each S (kill) script is executed with an argument of `stop`, and then each S (start) script is executed with an argument of `start`. Each of the K files is run in numerical order. The S files are run in similar fashion. This arrangement allows the person who sets up these files to control which services are stopped and which are started, and in what order, whenever the system enters a given runlevel. Using scripts with **start** and **stop** arguments promotes flexibility because it allows one script to both start and kill a process, depending on which argument it is called with.

To customize system initialization, you can add shell scripts to the `/etc/init.d` directory and place links to these files in the `/etc/rcn.d` directories (although in practice it is best to use `sysv-re-conf` [discussed next] to create the links).

The following example shows several links to the `cupsys` init script. These links are called to run the `cupsys` init script to start or stop the `cupsys` daemons at various runlevels:

```
`$ ls -l /etc/rc*/s*cupsys*` `lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc1.d/K80cupsys -> ../init.d/cupsys` `lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc2.d/S50cupsys -> ../init.d/cupsys` `lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc3.d/S50cupsys -> ../init.d/cupsys` `lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc4.d/S50cupsys -> ../init.d/cupsys` `lrwxrwxrwx 1 root root 14 2010-02-26 10:19 /etc/rc5.d/S50cupsys -> ../init.d/cupsys`
```

Each link in `/etc/rcn.d` points to a file in `/etc/init.d`. For example, the file `/etc/rc2.d/S50cupsys` is a link to the file named `cupsys` in `/etc/init.d`. (The numbers in the filenames of the links in the `/etc/rcn.d` directories may change from one release of Ubuntu to the next, but the scripts in `/etc/init.d` always have the same names.)
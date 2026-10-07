```
K10webmin    K34ypasswd    K86nfslock    S20apcupsd    S90vmware
K15httpd     K35dhcpd      K92ipchains   S20random     S90xfs
K15mysqld-sk  K35smbd      K96pcmcmd      S35identd     S91poststd
K15postgresql K44rawdevices S05kudzu      S55sshd       S95anacron
K20nfsv      K45named     S06reconfig    S56xinetd     S97rhnssd
K20rstatd    K72autofs    S08iptables    S60lpd        S991inuxconf
K20usersd    K74gpmdd     S10networl     S78mgsqid     S991local
K20rwalld    K74ypsserv   S12syslog      S80sendmail   S99webmin
```

You'll notice that each file begins with an S or a K. The system first runs the scripts whose names start with K to kill their associated processes, if running. Next, the system runs the scripts whose names start with S to start the associated processes. Changing a K name to start with S (such as renaming K20nfs to S20nfs) makes Linux start the process rather than kill it when entering the run level, and changing an S name to K causes Linux to kill the process when entering the run level. This is how Linux controls what processes to start in a given run level. Actually the files here are only symbolic links to the actual scripts which exist in /etc/rc/init.d.

> **Note** There are too many services running on this default install of Red Hat 7.3. See Chapter 15, "Security," for information about the security implications of having a lot of unnecessary processes running.

After the run level 3 processes are killed or started, the /sbin/update command in the inittab file is run. This command flushes the kernel buffers and writes their data to the hard drive. This is basic housekeeping to improve kernel performance.

The next line sets the Ctrl+Alt+Delete key combination to indicate a reboot of the system. Sometimes this is commented out on a system that is easily accessed to prevent allowing just anyone from rebooting it. The -t option indicates that the init process is to wait 3 seconds before telling its dependent processes to restart themselves. The shutdown occurs as if you had initiated the following shutdown command:

```
# /sbin/shutdown -t3 -r now
```

The pf line of the inittab file then sets the system up to run a different kind of shutdown if an attached uninterruptible power supply (UPS) indicates that power has failed. This shutdown is scheduled to occur 2 minutes after this notification. The following pr line, however, indicates that the shutdown is to be cancelled if the init process receives a notification that the power was restored before the shutdown was initiated. The pn line indicates still another type of shutdown for use when the UPS indicates low power.

The next six uncommented lines, with identifiers 1-6, run mingetty programs for the virtual terminals. These programs are essential since they initialize the ttys, provide the login and retrieve the user-input data, and then start a login process for the user. Without these lines, no users could log into the system.

The next to the last line, with the identifier of x, is set by the 5 in the second colon-delimited field to run the X Display Manager (XDM) process for run level 5 only. An XDM allows you to log into run level 5 directly. Red Hat 7.3 uses prefdm as its XDM program, but the program used varies from one distribution to another. KDE and GNOME each have their own display managers if you choose to use them; they are KDM and GDM respectively.

Finally, the last line respawns the Point-to-Point Tunneling Server daemon (pptpd), which allows virtual private network connections to be made to the Linux host.

66
# No graphics?

When you are working in text mode because you didn't get presented a graphical login screen on the console of your machine, you can normally switch to console 7 or up to have a graphical login. If this is not the case, check the current run level using the command **who -r**. If it is set to something else than the original default from `/etc/inittab`, chances are that the system does not start up in graphical mode by default. Contact your system administrator or read man init for that case. Note that switching run levels is done preferably using the **telinit** command; switching from a text to a graphical console or vice versa does not involve a run level switch.

The discussion of run levels, scripts and configurations in this guide tries to be as general as possible. Lots of variations exist. For instance, Gentoo Linux stores scripts in `/etc/run levels`. Other systems might first run through (a) lower run level(s) and execute all the scripts in there before arriving at the final run level and executing those scripts. Refer to your system documentation for more information. You might also read through the scripts that are referred to in `/etc/inittab` to get a better comprehension of what happens on your system.

# 4.2.5.1  Tools

The **chkconfig** or **update-rc.d** utilities, when installed on your system, provide a simple command-line tool for maintaining the `/etc/init.d` directory hierarchy. These relieve system administrators from having to directly manipulate the numerous symbolic links in the directories under `/etc/rc[x].d`.

In addition, some systems offer the **ntsysv** tool, which provides a text-based interface; you may find this easier to use than **chkconfig**'s command-line interface. On SuSE Linux, you will find the **yast** and **inserv** tools. For Mandrake easy configuration, you may want to try DrakConf, which allows among other features switching between run levels 3 and 5. In Mandriva this became the Mandriva Linux Control Center.

Most distributions provide a graphical user interface for configuring processes; check with your system documentation.

All of these utilities must be run as root. The system administrator may also manually create the appropriate links in each run level directory in order to start or stop a service in a certain run level.
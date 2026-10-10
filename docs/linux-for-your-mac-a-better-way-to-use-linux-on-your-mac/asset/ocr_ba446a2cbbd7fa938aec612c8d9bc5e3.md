![](bbox=[0.08, 0.08, 0.37, 0.28])

> Figure 3.2 KDE’s kcmclock client is used to set your timezone.

You can also set the time zone on the fly by creating or modifying the *TZ* environment variable, which is an in-memory setting that designates the current time zone (see the *tzset* manual page for details).

You can also update your system’s time through the Internet by using the *rdate* command and its *-s*, or *set*, option. This command can only be run by the root operator, and should be used with the name of an Internet time server, like this:

```
`# rdate -s tick.usno.navy.mil`
```

This command sets your Linux system time by retrieving the time from the specified remote server.

> > Unfortunately, the *rdate* command is not included with SuSE Linux PPC. However, you can download, build, and install this tiny utility from source code on the Internet.

# # Adding Users

Managing users on a Linux system is the job of the system administrator. But if you use Linux on a stand-alone workstation, you are the system administrator! One of your first jobs is to create a username and password for yourself, because you should not use Linux as the root operator (unless performing rescue operations or system maintenance).

Red Hat Linux-based systems include a variety of graphical and command-line tools used to create and manage users. SuSE Linux administrators can use the
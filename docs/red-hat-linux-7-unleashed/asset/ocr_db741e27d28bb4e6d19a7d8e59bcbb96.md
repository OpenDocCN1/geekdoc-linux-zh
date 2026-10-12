# System Startup and Shutdown



![](bbox=[0.21, 0.09, 0.48, 0.26])

+   * mailconf—A utility that configures the sendmail daemon
+   * netconf—A TCP/IP services configuration utility, as shown in Figure 9.3

![](bbox=[0.21, 0.36, 0.48, 0.71])

* userconf—User and group configuration (to add or delete users and groups)

Each program is a symbolic link to `linuxconf`. For example, to delete the user `clobje` from the command line, use `linuxconf`’s symbolic link `userconf`:

```
# userconf --deluser clobie
```

You can get help for each utility by using the `-help` command-line option, or if using X11, by clicking the Help button in the utility’s main dialog box.
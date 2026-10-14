another, you are taking your system from one configuration to another. SuSE Linux comes with six runlevels:

+   - runlevel 0 is halt.
+   - runlevel 5 is single-user.
+   - runlevel 1 is multi-user without network.
+   - runlevel 2 is multi-user with network.
+   - runlevel 3 is multi-user with network and xdm.
+   - runlevel 6 is reboot.

Runlevels 4 and 5 are left empty so that you can edit them yourself. Now the whole picture should be clearer. If you want to switch your system from runlevel 3 (multi-user with network and xdm) to runlevel S (single-user), all you have to do is tell init to do that. This is simply done by running the command:

```
# telinit runlevel
```

To switch to single-user, enter the following:

```
# telinit S
```

Runlevels are directories that hold the scripts required to bring the system to the configuration specified by the runlevel. Each runlevel has its own directory that contains symbolic links to the appropriate links in /sbin/init.d. Runlevel directories are found in /sbin/init.d/. Each runlevel has its own directory named rcX.d, where X is the number of the runlevel. So runlevel 3 is rc3.d.

Most of the time the order in which you call the scripts is important, which is why you can number them for init. If you look at any of the runlevel directories, you will see half the links start with SXXname and the other half with KXXname. S indicates that the script is to be run when starting the runlevel and K indicates a script that runs when killing the runlevel. The XX is a number that denotes the order of that script, starting from 01. For example, S06firewall is linked to /sbin/init.d/firewall, and means that this script is to be run as the sixth script.

When init is starting a runlevel, it calls all the links that start with S, with the start parameter as a command-line argument. This starts the correct scripts to bring the system up in a particular configuration. And when init switches runlevels, it first calls all the scripts that start with K in the current runlevel with stop as a command-line argument. init then calls the scripts of the new runlevel with start; remember that reboot and halt are runlevels as far as Linux is concerned.

Switching runlevels is done using the telinit command. Run telinit with the number of the runlevel you want to switch to as a command-line argument. For example, to switch to runlevel 2, you would enter the following:

```
bash# /sbin/telinit
```
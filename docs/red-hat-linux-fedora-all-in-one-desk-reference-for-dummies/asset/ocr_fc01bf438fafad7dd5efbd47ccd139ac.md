The first character of the output shows the previous run level (N means there is no previous run level), and the second character shows the current run level (5). In this case, the system was started at run level 5.

# Examining the /etc/inittab file

The /etc/inittab file is the key to understanding the processes that init starts at various run levels. You can look at the contents of the file by using the more command, as follows:

```
more /etc/inittab
```

![](bbox=[0.15, 0.38, 0.25, 0.52])

To see the contents of the /etc/inittab file with the more command, you don’t have to log in as root.

To interpret the contents of the /etc/inittab file, follow these steps:

+   1. Look for the line that looks like this:
+   ```
+   id:5:initdefault:
+   ```
+   That line shows the default run level. In this case, it’s 5.
+   
+   2. Find all the lines that specify what init should run at run level 5. Look for a line that has a 5 between the first two colons (:). Here are the two relevant lines:
+   ```
+   l5:5:wait:/etc/rc.d/rc 5
+   x:5:respawn:/etc/X11/prefdm -nodaemon
+   ```
+   The first line specifies that init should execute the file /etc/rc.d/rc with 5 as an argument. The second line causes init to run /etc/X11/prefdm, a shell script that starts the graphical display manager. The display manager, in turn, displays the graphical login dialog box that enables you to log in to the system.

If you look at the file /etc/rc.d/rc, you find it’s a shell script. You can study this file to see how it starts various processes for run levels 1 through 5.

Each entry in the /etc/inittab file tells init what to do at one or more run levels — you simply list all run levels at which the process should run. Each inittab entry has four fields — separated by colons — in the following format:

```
id:runlevels:action:process
```
```
# This does, of course, assume you have powerd installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -h +5 'Power Failure; System Shutting Down'

# If power was restored before the shutdown kicked in, cancel it.
po:12345:powerokwait:/sbin/shutdown -c 'Power Restored; Shutdown Cancelled'

# Run gettys in standard runlevels
1:12345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run kdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodeamon
```

# More About Runlevels

Now that you have an understanding of the init command, we can cover a topic we touched on briefly during our examination of the inittab file. We'll look at runlevels and managing the processes that run at each defined runlevel.

As stated earlier, Red Hat Linux uses a System V style of start scripts. This style differs from the BSD style in that each daemon or function to be started automatically by the system is controlled by a script that takes at least two possible arguments—start and stop.

For example, to start the Web server running on a system, a control script called httpd, web, or apache could be created that performs all of the actions required to start or stop the server depending on the argument given to the script. By separating each service or function into separate scripts, it becomes easier to define a runlevel. You simply have to decide which services and functions should be running at that runlevel and then start them using their control scripts. To do this, each runlevel has a directory in /etc/rc.d called rcN.d, where N is the runlevel, (rc3.d contains the collection of scripts that need to be run at this level). To further simplify matters, all of the scripts are collected into a central directory called /etc/rc.d/init.d.
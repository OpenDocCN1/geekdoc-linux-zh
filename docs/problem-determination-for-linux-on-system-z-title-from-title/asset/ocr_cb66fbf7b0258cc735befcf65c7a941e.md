+   - The starting service of each runlevel is set by the `chkconfig` command and the `inserv` command.

# Starting getty

+   - After starting all the daemons, getty is started.

Now we describe some parts of the /etc/inittab configuration file.

+   - The /etc/inittab format is id:runlevels:action:process.

+   - Some actions that the `init` command take when the process starts are:

+      - bootwait - The process is executed during system boot.

+      - initdefault - The default runlevel is configured here when the system starts.

+      - once - The process is started once when the specified runlevel is entered.

+   - The process starts only once when booting.

+      - wait - The process will be started once when the specified runlevel is entered and init will wait for its termination.

+      - respawn - The process will be restarted whenever it terminates.

See the /etc/inittab/ default configuration in Example 10-2.

# Example 10-2 Default configuration of /etc/inittab

```
# The default runlevel is defined here
id:5:initdefault:

# First script to be executed, if not booting in emergency (-b) mode
si::bootwait:/etc/init.d/boot

# /etc/init.d/rc takes care of runlevel handling
#
# runlevel 0  is  System halt   (Do not use this for initdefault!)
# runlevel 1  is  Single user mode
# runlevel 2  is  Local multiuser without remote network (e.g. NFS)
# runlevel 3  is  Full multiuser with network
# runlevel 4  is  Not used
# runlevel 5  is  Full multiuser with network and xdm
# runlevel 6  is  System reboot (Do not use this for initdefault!)
#
10:0:wait:/etc/init.d/rc 0
11:1:wait:/etc/init.d/rc 1
12:2:wait:/etc/init.d/rc 2
13:3:wait:/etc/init.d/rc 3
14:4:wait:/etc/init.d/rc 4
15:5:wait:/etc/init.d/rc 5
```
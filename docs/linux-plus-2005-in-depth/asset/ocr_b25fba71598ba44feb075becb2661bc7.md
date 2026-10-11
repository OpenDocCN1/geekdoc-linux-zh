# Trap CTRL-ALT-DELETE
ca::ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have power installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -f h +2 "Power Failure; System Shutting Down"

# If power was restored before the shutdown kicked in, cancel it.
pr:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
x:5:respawn:/etc/X11/prefdm -nodae
[root@server1 root]# _

The format of entries in the /etc/inittab file are as follows:

label : runlevel(s) : action : command

The label is just an identifier that allows the init daemon to examine this file in alphabetical order; the runlevel specifies to which runlevel the line in /etc/inittab corresponds; the command tells the init daemon what to execute when entering the runlevel; and the action tells the init daemon how to execute the command.

Thus, the line id:5:initdefault: in the /etc/inittab file tells the init daemon that runlevel 5 is the default runlevel to boot to when initializing the Linux system at system startup. In addition, the si::sysinit:/etc/rc.d/rc.sysinit line tells the init daemon to run the program /etc/rc.d/rc.sysinit before entering a runlevel at system initialization. This program initializes the hardware components of the system, sets environment variables such as PATH and HOSTNAME, checks file systems, and performs system tasks required for daemon loading. The output from the /etc/rc.d/rc.sysinit program is displayed on the terminal screen during system startup as soon as the graphical boot starts; simply click Show Details at the graphical boot screen to see the individual actions.

Because the default runlevel is 5, only the line 15:S:wait:/etc/rc.d/rc 5 will be executed in the next section of the /etc/inittab file seen earlier. This line executes the /etc/rc.d/rc 5 command and waits for it to finish before proceeding to the rest of the /etc/inittab file. The
```
# 6 - reboot (Do NOT set initdefault to this)
#
id:3:initdefault:

# System initialization.
si::sysinit:/etc/rc.d/rc.sysinit

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6

# Things to run in every runlevel.
ud:once:/sbin/update

# Trap CTRL-ALT-DELETE
ca:ctrlaltdel:/sbin/shutdown -t3 -r now

# When our UPS tells us power has failed, assume we have a few minutes
# of power left.  Schedule a shutdown for 2 minutes from now.
# The following lines were added on 9/17/01 for a CyberPower 700 AVR UPS

#UPS signals a power outage.
pf:12345:powerfail:/sbin/powstatd.fail

# UPS signals power restored before the shutdown kicks in.
pr:12345:powerokwait:/sbin/powstatd.ok

# UPS signals low battery power: emergency shutdown.
pn:12345:powerfailnow:/sbin/powstatd.low

# Run gettys in standard runlevels
1:2345:respawn:/sbin/mingetty tty1
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6

# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdm -nodaemon
p:1:respawn:/usr/sbin/moused -Q
```

The file begins with a block of comments, including a summary of the run levels used in Red Hat; let’s take a moment to look at the six run levels and their uses:

|0|Used to halt the system. To do this, the system performs an INIT 0 command and the system is halted. as the comment says, you should not set initdefault to this.|

|1|Puts the system into single-user mode.|

|2|Puts the system into a multiuser mode but does not support networking.|

|3|Puts the system into the standard full multiuser mode but does not automatically start X.|

|4|Unused|

|5|X11: puts the system into standard multiuser mode with a graphical (X-based) login.|
# LISTING 13.1 CONTINUED

```
```text
~1:S:wait:/etc/rc.d/rc 1
~~:S:wait:/sbin/sulogin

10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
# Normally not reached, but fallthrough in case of emergency.
z6:6:respawn:/sbin/sulogin

# Trap CTRL-ALT-DELETE
ca:12345:ctrlaltdel:/sbin/shutdown -t3 -r now

# Action on special keypress (ALT-UpArrow).
kb::kbrequest:/bin/echo "Keyboard Request --edit /etc/inittab to let this work."

# When our UPS tells us power has failed, assume we have a few minutes
# of power left. Schedule a shutdown for 2 minutes from now.
# This does, of course, assume you have power installed and your
# UPS connected and working correctly.
pf::powerfail:/sbin/shutdown -h +5 "Power Failure; System Shutting Down"

# If battery is fading fast -- we hurry...
p1::powerfailnow:/sbin/shutdown -c 2> /dev/null
p2::powerfailnow:/sbin/shutdown -h now "Battery Low..."

# If power was restored before the shutdown kicked in, cancel it.
po:12345:powerokwait:/sbin/shutdown -c "Power Restored; Shutdown Cancelled"

# Run gettys in standard runlevels
1:12345:respawn:/sbin/getty tty1 VC linux
2:2345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux

# Run kdm in runlevel 5
gu:5:respawn:/bin/sh -c "C=/etc/rc.d/rc.gui;[ -x $C ]&&exec $C;init 3"
```
```

> Runlevels are just a convenient way to group together process packages using software. They hold no special significance to the kernel. All Linux kernels start the boot process the same way. It’s only after init starts that you begin to use runlevels.
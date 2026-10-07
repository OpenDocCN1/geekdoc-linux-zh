v.4.33                               A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
id:3:initdefault:
nbarry@forensic1:-$ cat /etc/inittab
<previous output>
# These are the default runlevels in Slackware:
# 0 = halt
# 1 = single user mode
# 2 = unused (but configured the same as runlevel 3)
# 3 = multiuser mode (default Slackware runlevel)
# 4 = X11 with KDM/GDM/XDM (session managers)
# 5 = unused (but configured the same as runlevel 3)
# 6 = reboot

# Default runlevel. (Do not set to 0 or 6)
id:3:initdefault:
```

# System initialization (runs when system boots)
si:S:sysinit/etc/rd/rc.S

It is here that the default runlevel for the system is. If you want a text login (which I suggest), set the above value in initdefault to “3”. This is the default for Slackware. With this default runlevel, you use startx to the X Window GUI system. If you want a graphical login, you would edit the above line to a “d".

Note that for Ubuntu, you can create an /etc/inittab file and place the value there. If it exists, the runlevel changed accordingly. The systemd method of management used by Ubuntu does not really utilize “runlevels”. It utilizes targets. Changes to these targets are made using the systemctl command. The configuration and use of Ubuntu is outside the scope of this guide, but this particular issue highlights the fact that Linux systems can vary in how they work.

# Global Startup Scripts

After the default run level has been set, init (via /etc/inittab) then runs the following scripts:

+   - /etc/rd.d/rc.S - handles system initialization, file system mount and encrypted volumes, swap initialization, devices, etc.
- /etc/rd.d/rc.-X - X is the runlevel passed as an argument to init. In the case of multiuser (non GUI) logins (run level 2 or 3), this is rc.M. This script then calls other startup scripts (various services, etc.) by checking to see if they are “executable".
- /etc/rd.d/rc.local - called within the specific run level scripts, rc.local is a general purpose script that can be edited to include commands that you wanted at boot up.
- /etc/rd.d/rc.local_shutdown - This file be used to stop any

43
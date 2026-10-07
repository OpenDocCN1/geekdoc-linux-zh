If /etc/inittab contained any additional lines that specified no run level (meaning to run at boot time only) or run level 3, they would be run. You can add any such lines yourself, if you have something that you need to start only in a certain run level. Usually the Red Hat default inittab is fine as it comes.

You don't typically customize the rc.sysinit file or the run level scripts, since the rc.local file was included for that purpose. It is run next. This is the file where you make your local changes to the startup process. This file runs after all of the other initialization files and can therefore be used to override any settings made during the earlier initialization steps. By default, this file creates the login banners /etc/issue and /etc/issue.net. These files are used to set the display that will precede the login prompt when a user logs in locally (/etc/issue) or remotely (/etc/issue.net). By default, the /etc/issue file contains something like this:

Red Hat Linux release 7.3 (Valhalla)

Many system administrators think this is too much information to give to someone who may be trying to crack your system. It might be better to change the /etc/issue banner to something more generic like "Welcome to localhostdomain" or to give your users any information you believe they need before entering your system. If you change the /etc/issue file directly, it will be overwritten when the /etc/rc.d/rc.local file is run again. You must change this in /etc/rc.d/rc.local to make the change permanent. Since this file is one big if clause, any commands that you wish to add should be added before the last fi.

# ## The Debian Model

Debian's inittab file is only slightly different from Red Hat's version. Listing 3.5 shows a sample Debian inittab.

Listing 3.5: Debian's inittab File

```
# /etc/inittab: init(8) configuration.
# $Id: inittab,v 1.8 1998/05/10 10:37:50 miquels Exp $

# The default runlevel.
id:2:initdefault:

# Boot-time system configuration/initialization script.
# This is run first except when booting in emergency (-b) mode.
si::sysinit:/etc/init.d/rcS

# What to do in single-user mode.
~~:S:wait:/sbin/sulogin

# /etc/init.d executes the S and K scripts upon change
# of runlevel.
#
# Runlevel 0 is halt.
# Runlevel 1 is single-user.
# Runlevels 2-5 are multi-user.
# Runlevel 6 is reboot.

10:0:wait:/etc/init.d/rc 0
11:1:wait:/etc/init.d/rc 1
12:2:wait:/etc/init.d/rc 2
13:3:wait:/etc/init.d/rc 3
14:4:wait:/etc/init.d/rc 4
15:5:wait:/etc/init.d/rc 5
```

67
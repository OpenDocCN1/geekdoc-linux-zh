```
# Copyright (c) 1999, 2000 Red Hat, Inc.

pifodof -s kdm > /dev/null 2>&1
if [ $ -eq 0 -a ~/usr/bin/kdmesktop ]; then
/usr/bin/kmdesktop
else
/usr/X11R6/bin/xsetroot -solid "#356390"
fi

# only set the background if the xsri program is installed
if [ -x /usr/bin/xsri ]; then
/usr/bin/xsri -geometry +5+5 -avoid 300x250 -keep-
aspect \
/usr/share/pixmaps/redhat/redhat-transparent.png
fi
```

This file starts the xconsole and xbanner programs when a user is authenticated. These are practically useless for most users. Hence you should modify this to whatever is appropriate. For example, you might use the xv program to set the background of the X environment to something appropriate for your organization. Or perhaps you can start up a few applications that are typically run by most users, such as the xmailbox.

The xdm can be run automatically after boot by changing the default run level to 5. To change the run level of your system to 5, modify the following line in the /etc/inittab file:

```
id:3:initdefault:
```

Replace the 3 with 5. And make sure that you have the following lines in the same file:

```
# Run xdm in runlevel 5
# xdm is now a separate service
x:5:respawn:/etc/X11/prefdmd -nodaemon
```
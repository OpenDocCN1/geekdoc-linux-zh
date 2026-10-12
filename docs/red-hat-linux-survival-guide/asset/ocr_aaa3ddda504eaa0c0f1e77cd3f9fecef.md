your answer. Using xdm you can authenticate users via a graphical login screen and take them straight to their X Window environment. The purpose of this program is to provide services similar to getty and login. You can start the display manager as follows:

```
xdm &
```

The xdm configuration files are located in the /usr/X11R6/lib/X11/xdm directory. The file xdm-config is for configuring how the login screen appears to users, and Xsetup_0 is used to tell xdm what programs should be launched when X is started. The default Xsetup_0 is shown here:

```
#!/bin/sh
# Xsetup for Red Hat Linux
# Copyright (c) 1999, 2000 Red Hat, Inc.

pidof -s kdm > /dev/null 2>&1
if [ $? -eq 0 -a -x /usr/bin/kdmdesktop ]; then
    /usr/bin/kdmdesktop
else
    /usr/X11R6/bin/xsetroot -solid "#356390"
fi

# only set the background if the xsri program is installed
if [ -x /usr/bin/xsri ]; then
    /usr/bin/xsri -geometry +5+5 -avoid 300x250 -keep-aspect \
        /usr/share/pixmaps/redhat/redhat-transparent.png
fi
```

This file starts the xconsole and xbanner programs when a user is authenticated. These are practically useless for most users. Hence you should modify this to whatever is appropriate. For example, you might use the xv program to set the background of the X environment to something appropriate for your organization. Or perhaps you can start up a few applications that are typically run by most users, such as the xmailbox.
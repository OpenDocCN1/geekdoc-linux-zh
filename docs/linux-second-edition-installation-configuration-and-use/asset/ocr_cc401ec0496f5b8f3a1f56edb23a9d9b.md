# SELECTING YOUR WINDOW MANAGER OR DESKTOP ENVIRONMENT 269

```
#!/bin/sh
# xinitrc minimal version
# "/.xinitrc or /etc/x11/xinitrc/xinitrc
#
or /usr/X11R6/lib/X11/xinitrc/xinitrc
xterm -ls -geometry 80x30+10+10 &\ # shell window
exec fwm
```

Normally, xinitrc is slightly more complex. On the one hand, it contains code that causes Xresources and Xmodmap files to be read in automatically. On the other hand, in some distributions, it contains code that starts the file ~/.clients of the programs directly specified in xinitrc. This allows you to create clients in the home directory for a private configuration (and otherwise use the global xinitrc). The following list shows a modified version of xinitrc for RedHat

```
#!/bin/sh
# xinitrc example (RedHat)
# XConsortium:xinitrc.cpp,v 1.4 91/08/22 11:41:34 rws Exp $
userresources=$HOME/.Xresources
usermap=$HOME/.Xmodmap
sysresources=/usr/X11R6/lib/X11/.Xresources
sysmodmap=/usr/X11R6/lib/X11/.Xmodmap
# if local or global Xmodmap files (rarely) and for
# resources files (frequently) exist, they are loaded
if [ -f $sysresources ]; then
rdb -merge $sysresources
fi
if -f $sysmodmap ]; then
xmodmap $sysmodmap
fi
if -f $userresources ]; then
rdb -merge $userresources
fi
if -f $usermap ]; then
xmodmap $usermap
fi
# if "/.Clients exists execute
if [ -f $HOME/.clients ]; then
exec $HOME/.clients
elif [ -f /etc/x11/xinit/Xclients ]; then
exec /etc/x11/xinit/Xclients
else
clock -geometry 50x50-1+1 &
xterm -geometry 80x50+494+51 &
xterm -geometry 80x20+494-0 &
if [ -f /usr/X11R6/bin/fwm ]; then
exec fwm
else
exec twm
fi
```
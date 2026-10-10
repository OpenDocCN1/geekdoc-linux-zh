```
if test -n "$WINDOWMANAGER" ; then
    WINDOWMANAGER=`type -p $WINDOWMANAGER`
fi
if test -z "$WINDOWMANAGER" ; then
    if test -x /usr/X11R6/bin/kde ; then
        WINDOWMANAGER=/usr/X11R6/bin/kde
    elif test -x /usr/X11R6/bin/startkde ; then
        WINDOWMANAGER=/usr/X11R6/bin/startkde
    elif test -x /usr/X11R6/bin/fvwm2 ; then
        WINDOWMANAGER=/usr/X11R6/bin/fvwm2
    elif test -x /usr/X11R6/bin/wmlist ; then
        for i in '/usr/X11R6/bin/wmlist' ; do
            WINDOWMANAGER=`type -p $i`
            test -n "$WINDOWMANAGER" && break
        done
    fi
fi
...
```

In this example, the script checks for a designated window manager in the WINDOWMANAGER environment variable, and checks to see if its name is present in the system-wide list of window managers stored under the /usr/X11R6/bin directory. Other distributions, such as LinuxPPC 2000 Q4 may use a different scheme, such as using a script named xclients under the /etc/X11/xinit directory to parse the contents of the /etc/sysconfig/desktop file for a default window manager. This latter approach is used by a number of Red Hat-based Linux distributions, and the logic looks like this:

```
...
```

```
# check to see if the user has a preferred desktop
PREFERRED=
if [ -f /etc/sysconfig/desktop ]; then
    if [ -n "`grep -i Gnome /etc/sysconfig/desktop`" ]; then
        PREFERRED=gnome-session
    elif [ -n "`grep -i KDE /etc/sysconfig/desktop`" ]; then
        PREFERRED=startkde
    elif [ -n "`grep -i AnotherLevel /etc/sysconfig/desktop`" ]; then
        PREFERRED=AnotherLevel
    else
        PREFERRED=Default
    fi
fi
```

```
...
```
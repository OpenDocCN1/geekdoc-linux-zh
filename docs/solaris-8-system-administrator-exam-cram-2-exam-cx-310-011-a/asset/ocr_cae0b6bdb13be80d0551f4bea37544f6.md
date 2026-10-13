```
```sh
if [ `tty` = "/dev/console" ] ; then
        if [ "$TERM" = "sun" -o "$TERM" = "sun-color"
        -o "$TERM" = "AT386" ]
        then
                if [ ${OPENWINHOME:-""} = "" ] ; then
                        OPENWINHOME=/usr/openwin
                        export OPENWINHOME
                fi
                echo ""
                echo "Starting OpenWindows in 5 seconds"
                sleep 5
                echo ""
                $OPENWINHOME/bin/openwin
                clear # get rid of annoying cursor rectangle
                exit # logout after leaving windows system
        fi
fi
```
```

For user accounts that use csh as the login shell, the /etc/skel/local.login file is copied to the .login file in the user’s home directory. The following example shows the default contents of the /etc/skel/local.login file:

```
```csh
stty -istrip
# setenv TERM 'tset -Q .'
#
# if possible, start the windows system.
#
if ( `tty` == "/dev/console" ) then
        if ( "$TERM" == "sun" || "$TERM" == "sun-color"
             || "$TERM" == "AT386" ) then
                if ( ${OPENWINHOME} == 0 ) then
                        setenv OPENWINHOME /usr/openwin
                endif
                echo ""
                echo -n "Starting OpenWindows in 5 seconds"
                sleep 5
                echo ""
                $OPENWINHOME/bin/openwin
                clear # get rid of annoying cursor rectangle
                logout # logout after leaving windows system
        endif
endif
```
```

In addition, for user accounts that use csh as the login shell, the /etc/skel/.cshrc file is copied to the .cshrc file in the user’s home directory. The following example shows the default contents of the /etc/skel/.cshrc file:

```
```csh
umask 022
set path=(/bin /usr/bin /usr/ucb /etc .)
if ( $?prompt ) then
        set history=32
endif
```
```

The /etc/skel directory also contains a simple .profile that can be used as a default.
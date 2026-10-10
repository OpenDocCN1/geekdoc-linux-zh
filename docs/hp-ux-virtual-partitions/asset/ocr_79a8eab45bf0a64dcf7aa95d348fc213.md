example. The default information for the login screen is contained in `/usr/dt/config/C/Xresources`. We’ll copy this file to the home directory and `.dt` directory for root, which, on this `vPar`, is `/root/.dt`. We’ll rename the file `dtwmrc` after copying it. The menu portion of `/root/.dt/dtwmrc` looks like the following before it is updated:

```
Menu DtRootMenu
{
   "Workspace Menu"                       f.title
   "Shuffle Up"                           f.circle_up
   "Shuffle Down"                         f.circle_down
   "Refresh"                              f.refresh
   "Minimize/Restore Front Panel"         f.toggle frontpanel
   no-label                               f.separator
   "Restart Workspace Manager..."         f.restart
   no-label                               f.separator
   "Log out..."                           f.action ExitSession
}
```

We’re going to add our new menu pick just after the `DtRootMenu` entry, which we see on our system as the left mouse button’s “Workspace Menu.” After adding our menu picks the file now looks like the following:

```
Menu DtRootMenu
{
   "Workspace Menu"                       f.title
   "Shuffle Up"                           f.circle_up
   "Shuffle Down"                         f.circle_down
   "Refresh"                              f.refresh
   "Minimize/Restore Front Panel"         f.toggle frontpanel
   no-label                               f.separator
   "Restart Workspace Manager..."         f.restart
   no-label                               f.separator
   "Log out..."                           f.action ExitSession

Menu vParMenu
   "vPar Menu"                            f.title
   "vparstatus"                           f.exec "xterm -T vparstatus -e
                                               /usr/bin/sh -c `vparstatus; read xxx"`
   "vparstatus -v"                        f.exec "xterm -geometry 80x50-55+0
                                               -sl 200 -bg white -T vparstatus_verbose
                                               -e /usr/bin/sh -c `vparstatus -v;more; read xxx"`
   "Login vPar2"                          f.exec "xterm -geometry 80x50-55+0 -sl 200 -bg white
                                               -T vPar2 -e remsh vpcvarpd 2 &"
}
```
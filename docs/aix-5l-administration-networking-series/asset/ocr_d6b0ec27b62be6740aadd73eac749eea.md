on an X-server that does not support the X Display Manager Control Protocol (XDMCP) by adding the following line to the Xserveds file:

```
<hostname_of_xterminal>:0 foreign /usr/lpp/X11/bin/X -T -force
```

The *xaccess* file can limit what hosts have access to directly or indirectly access the login GUI. To limit only *MyXterminal* access to the display manager, comment out the following two lines that begin with an asterisk (*) and add the two *MyXterminal* lines to replace them in the *Xserveds* file:

```
#* \———————Grant service to all
MyXterminal_DomainName
#*    CHOOSER  BROADCAST  \—————Any indirect host can get a chooser
MyXterminal_DomainName                CHOOSER  BROADCAST
```

The display managers invoke the *Xsession* file to set up the desktop environment and resources. The *xdlogin* display manager treats the *Xsession* file as an executable script and stores it in a different location from the configuration files as /usr/dt/bin/Xsession. The *xdm* and *kdm* display managers provide for sourcing the /etc/profile, *$HOME/.profile*, and *$HOME/.login* files, whereas *xdlogin* provides no sourcing of /etc/profile from the *Xsession* file and only a hook from *$HOME/.dprofile* that allows users to source their own * .profile* or *.login* files when DTSOURCEPROFILE is true. The *Xsession* file for the *kdm* display manager will source the profile files before calling the /usr/dt/bin/Xsession script if you select CDE as your desktop.

# START AND STOP DISPLAY MANAGERS

Each of the three display managers can be started by an entry in the /etc/inittab file at system boot time or from the command line, and that is how you started the one you use, then you may stop it, if needed, by simply killing the PID found in the appropriate xdm-pid file. I like to keep a line for each display manager in the /etc/inittab file with only the one I use, at system boot, uncommented. My entries look like this:

```
xdm:2:wait:/usr/lpp/X11/bin/xdm        # Starts XDM as daemon
kdm:2:wait:/opt/freeware/kde/bin/kdm   # Starts KDM as daemon
dt:2:wait:/etc/rc.dt                   # Starts xdlogin as daemon
dt_nogb:2:wait:/etc/rc.dtd             # Starts xdlogin as system resource
```

To stop them after system boot has started your preferred display manager, use one of the following commands:

```
# kill -term $(cat /usr/lpp/X11/lib/X11/xdm/xdm-pid) \—————Stops xdm
# kill -term $(cat /opt/freeware/kde/share/config/kdm/xdm-pid) \—Stops kdm
# kill -term $(cat /var/dt/Xpids) \—————Stops xdlogin
```
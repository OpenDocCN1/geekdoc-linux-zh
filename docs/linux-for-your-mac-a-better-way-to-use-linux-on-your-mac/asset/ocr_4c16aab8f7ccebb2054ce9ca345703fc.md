![](bbox=[0.15, 0.05, 0.5, 0.25])

time zone database. Under SuSE Linux, you can set your time zone by editing its system-wide configuration file, /etc/rc.config. Look for the following entry:

```
TIMEZONE=EST
```

After making changes, make sure to run SuSE’s suseconfig shell script to implement your change.

SuSE Linux also provides a console-based, comprehensive system administration tool named yast, along with a newer graphical version for X11 named yast2. When you use the yast command, you can jump right to a specific administrative task by using its --mask option, followed by a keyword such as backup, consolefont, gpm, help, keymap, modem, mouse, netprinter, printer, scanner, timezone, user, or ffree. To jump right to an easy time zone configuration, use yast, like this: yast --mask timezone.

![](bbox=[0.03, 0.59, 0.13, 0.66])

System administrators using KDE can use the kcmclock client to set the time and designate a time zone. Start the client from the command line of an X11 terminal window, like this:

```
# kcmclock &
```

When the client starts, click the time zone tab in the dialog box, as shown in Figure 3.2.

Click the drop-down GMT menu and select your time zone (as an offset to GMT).
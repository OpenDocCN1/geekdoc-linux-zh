devices can be used with Red Hat Linux and XFree86, for information about using a mouse with XFree86, read the file README.mouse under a /usr/X11R6/lib/X11/doc directory.

Mouse support for copy and paste operations in a Linux console session is provided by the Linux General Purpose Mouse driver (gpm). gpm is a daemon, or software that runs in memory as a background process while you use Red Hat. If you make the appropriate configuration choices, the /etc/rc.d/init.d/gpm script starts when Red Hat boots. If you're not using X, you can configure Red Hat Linux to start gpm when booting using the ntsysv command from the console. Run the ntsysv command at root, like this:

```
# ntsysv
```

After you press Enter, you'll see the Services dialog box, as shown in Figure 4.4.

![](bbox=[0.303, 0.365, 0.663, 0.597])

FIGURE 4.4 Use the ntsysv command to produce the Services dialog, in which you can configure the gpm driver to start at boot time.

Scroll through the list of services using the Up or Down cursor keys to highlight the gpm service. Press the spacebar to toggle the service on (an asterisk will appear between the brackets) or off (no asterisk). Then tap the Tab key to highlight the OK button and press Enter to save your changes. The changes will take effect the next time you boot Red Hat.

> You can use the chkconfig command or the redhat-config-services client to configure Red Hat Linux to run the gpm daemon when you're working in console mode (but not during X Window System sessions). Use the chkconfig command like this:
# chkconfig --level 3 gpm on
# chkconfig --level 5 gpm off

See Chapter 7, "Managing Services," to see how to configure when services run under Red Hat.
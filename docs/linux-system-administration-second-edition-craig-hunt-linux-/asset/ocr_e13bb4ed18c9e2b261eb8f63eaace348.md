```
2:2345:respawn:/sbin/mingetty tty2
3:2345:respawn:/sbin/mingetty tty3
4:2345:respawn:/sbin/mingetty tty4
5:2345:respawn:/sbin/mingetty tty5
6:2345:respawn:/sbin/mingetty tty6
```

Each line in the /etc/inittab file contains colon-delimited entries that tell the system to run specific types of services. The preceding entries tell Linux to run the /sbin/mingetty program for each of the first six virtual consoles in run levels 2 through 5. The result of these entries is that you can type Alt+1 through Alt+6 (in combination with Ctrl, if you're currently running X) to shift to any of six virtual consoles. You can log in to any of these to run programs, even under different usernames.

To expand the default configuration to support terminals run over a serial port, it's necessary to add some further entries to /etc/inittab. To do so, follow these steps:

+   Install the mggetty package. On a Red Hat 7.3 system, the package name is mggetty-1.1.28-3.i386.rpm, and it's on the second CD-ROM.

> Different distributions use different getty programs by default. Red Hat's mingetty can't handle serial port traffic, but some default getty programs can handle the serial port, so this step may not be necessary with all distributions. If you use something other than mggetty, however, some of the following details may differ; consult your getty program's documentation for details.

+   To add support for a terminal attached to /dev/ttyS0, add the following line to /etc/inittab just after the existing mingetty lines:

```
S0:2345:respawn:/sbin/mggetty -s 57600 -r /dev/ttyS0
```

+   Type telinit Q to tell Linux to reexamine the /etc/inittab file and make appropriate changes—namely, to run mggetty.

You may need to make adjustments to step 2 for your particular needs. Specifically, step 2 runs the terminal at 57,600bps (the -s 57600 parameter) and uses /dev/ttyS0. Using higher speeds may make sense with some modems or direct links, but some terminals only support lower speeds. The -r parameter indicates that the connection is direct—that is, not via a modem. Modem logins, as described shortly, require a few changes to this configuration.

Once logged on using a terminal, the user can run Linux text-mode programs, including text-based administrative tools (assuming the user has sufficient privileges, of course). Some programs, however, rely on text-positioning protocols. These protocols were originally used with particular models of dumb terminals, and so are frequently named after those terminals. Examples include VT-100 and VT-220. In many cases, mggetty can determine the type of terminal that's connected. In other cases, you may need to do this manually by setting the TERM environment variable. For instance, if you're using a VT-100 terminal, you could type the following after logging in:

```
$ export TERM=vt100
```

If you find that your display does strange things, type echo $TERM to see what the system thinks the terminal type is, and adjust it as appropriate. Some dumb terminals emulate others, and most terminal programs emulate one or more popular dumb terminals.
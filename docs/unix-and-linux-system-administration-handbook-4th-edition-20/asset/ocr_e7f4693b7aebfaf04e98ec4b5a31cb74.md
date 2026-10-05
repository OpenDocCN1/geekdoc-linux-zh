# Chapter 31 Serial Devices and Terminals

speed is the baud rate (e.g., 38400), device is the device file for the serial port (use the full pathname).

If you want to specify a default terminal type for a port when using mtty, you must specify it in a separate file, /etc/ttytype, and not on the mtty command line. The format of an entry in ttytype is described on page 112.

# Ubuntu Upstart

Ubuntu has replaced its init with a rearchitected version called Upstart that starts and stops services in response to events. The executable file for Upstart is still known as /sbin/init,

Upstart uses one file for each active terminal in /etc/event.d. For example, if we wanted a getty to run on ttyS0etc/event.d/ttyS0 might look like this:

```
# ttyS0 - getty
# This service maintains a getty from ttyS0 from the point when
# the system is started until it is shut down again.
```

```
start on runlevel 2
start on runlevel 3
start on runlevel 4
start on runlevel 5

stop on runlevel 0
stop on runlevel 1
stop on runlevel 6 respawn
exec /sbin/getty 38400 tty0
```

See page 94 for some additional comments about Upstart.

# Solaris and sacadam

Rather than traditional UNIX get { that watch each port for activity and provide a login prompt, Solaris has a convoluted hierarchy called the Service Access Facility that controls TTY monitors, port monitors, and many other things that provide a lot of complexity but little added functionality.

To set up a serial port to provide a login prompt, you must first configure a "monitor" that watches the status of the port (ttymon). You then configure a port monitor that watches the TTY monitor. For example, to set up a 9,600 baud monitor on tty to bind a login prompt with terminal type VTY100, you might use the following commands.

```
solaris$ sudo sacadam -a -p mttymon -t ttymon /usr/lib/saf/ttymon -v 1
solaris$ sudo pmadm -a -p mttymon -s b -1 root -v 1 m "tty" -d
/dev/term/b -1 9600 -t vt100 -s /usr/bin/login
```

The /etc/ttydefs file is used much like gettydefs on other systems to set speed and parity parameters.
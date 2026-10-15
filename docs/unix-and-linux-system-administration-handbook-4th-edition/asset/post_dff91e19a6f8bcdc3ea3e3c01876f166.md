
*speed* is the baud rate (e.g., 38400), and *device* is the device file for the serial port (use the full pathname).

If you want to specify a default terminal type for a port when using **mgetty**, you must specify it in a separate file, **/etc/ttype**, and not on the mgetty command line. The format of an entry in **ttype** is described on page 1172.

## Ubuntu Upstart

Ubuntu has replaced its **init** with a rearchitected version called Upstart that starts and stops services in response to events. The executable file for Upstart is still known as **/sbin/init**, however.

Upstart uses one file for each active terminal in **/etc/event.d**. For example, if we wanted a getty to run on ttyS0, **/etc/event.d/ttyS0** might look like this:

```
# ttyS0 — getty

# This service maintains a getty on ttyS0 from the point when
# the system is started until it is shut down again.

start on runlevel 2
start on runlevel 3
start on runlevel 4
start on runlevel 5

stop on runlevel 0
stop on runlevel 1
stop on runlevel 6 respawn
exec /sbin/getty 38400 ttyS0
```

See page 94 for some additional comments on Upstart.

## Solaris and sacadm

Rather than traditional UNIX gettys that watch each port for activity and provide a login prompt, Solaris has a convoluted hierarchy called the Service Access Facility that controls TTY monitors, port monitors, and many other things that provide a lot of complexity but little added functionality.

To set up a serial port to provide a login prompt, you must first configure a “monitor” that watches the status of the port (**ttymon**). You then configure a port monitor that watches the TTY monitor. For example, to set up a 9,600 baud monitor on **ttyb** to print a login prompt with terminal type VT100, you would use the following commands.

```
solaris$ sudo sacadm -a -p mytmon -t ttymon -c /usr/lib/saf/ttymon -v 1
solaris$ sudo pmadm -a -p mytmon -s b -i root -fu -v 1 -m "ttymon -d /dev/term/b -l 9600 -T vt100 -s /usr/bin/login"
```

The **/etc/ttytab** file is used much like gettydefs on other systems to set speed and parity parameters.

See the manual pages for saf, sacadm, pmadm, ttyadm, and ttymon as well as the terminals chapter in the Solaris AnswerBook for more information about setting up these monitors. Have fun.

## 31.9 SPECIAL CHARACTERS AND THE TERMINAL DRIVER

The terminal driver supports several special functions that you access by typing particular keys (usually control keys) on the keyboard. The exact binding of functions to keys can be set with the tset and stty commands. Table 31.6 lists some of these functions, along with their default key bindings.

### Table 31.6 Special characters for the terminal driver

| Name | Default | Function |
|---|---|---|
| erase | <Control-?> | Erases one character of input |
| werase | <Control-W> | Erases one word of input |
| kill | <Control-U> | Erases the entire line of input |
| eof | <Control-D> | Sends an "end of file" indication |
| intr | <Control-C> | Interrupts the currently running process |
| quit | <Control-\> | Kills the current process with a core dump |
| stop | <Control-S> | Stops output to the screen |
| start | <Control-Q> | Restarts output to the screen |
| susp | <Control-Z> | Suspends the current process |
| lnext | <Control-V> | Interprets the next character literally |

Depending on what a vendor's keyboards look like, the default for ERASE might be either <Control-H> or the delete character. (The actual keyboard key may be labeled "backspace" or "delete," or it may show only a backarrow graphic.) Unfortunately, the existence of two different standards for this function creates a multitude of problems.

You can use stty erase (see the next section) to tell the terminal driver which key code your setup is actually generating. However, some programs (such as text editors and shells with command-editing features) have their own idea of what the backspace character should be, and they don't always pay attention to the terminal driver's setting. In a helpful but confusing twist, some programs obey both the backspace and delete characters. You may also find that systems you log in to through the network make different assumptions from those of your local system.

Solving these annoying little conflicts can be a Sunday project in itself. In general, there is no simple, universal solution. Each piece of software must be individually beaten into submission. Two useful resources to help with this task are the Linux Backspace/Delete mini-HOWTO from tldp.org and a nitty article by Anne Baretta at ibb.net/~anne/keyboard.html. These notes are both written from a Linux perspective, but the problem (and solutions) are not limited to Linux.

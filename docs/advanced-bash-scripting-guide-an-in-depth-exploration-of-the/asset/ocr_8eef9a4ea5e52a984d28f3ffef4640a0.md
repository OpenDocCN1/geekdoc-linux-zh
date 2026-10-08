# Advanced Bash-Scripting Guide

# Good for portable cross-platform scripts,
# where the Perl binaries may not be in the expected place.
# Thanks, S.C.
Or even ...

```
#!/bin/env bash
# Queries the PATH envimental variable for the location of bash.
...
# This script will run where Bash is not in its usual place, in /bin.
...
```

Show shared library dependencies for an executable file.

```
bash$ ldd /bin/ls
libc.so.6 => /lib/libc.so.6 (0x0400c000)
/ /lib/ld-linux.so.2 => /lib/ld-linux.so.2 (0x08000000)
```

Run a command repeatedly, at specified times.

The default is two-second intervals, but this may be changed with the -n option.

```
watch -n 5 tail /var/log/messages
# Shows tail end of system log, /var/log/messages, every five seconds.
```

Unfortunately, piping the output of watch command to grep does not work.

Remove the symbolic references from an executable binary. This decreases its size, but makes debugging it impossible.

This command often occurs in a Makefile, but rarely in a shell script.

List symbols in an uncompiled binary.

Command-line tool for manipulating the root window of the screen.

**Example 17-11. Backlight:** changes the brightness of the (laptop) screen backlight

```
#!/bin/bash
# backlight.sh
# reldate 02dec2011

# A bug in Fedora Core 16/17 messes up the keyboard backlight controls.
# This script is a quick-dirty workaround, essentially a shell wrapper
# for xrandr. It gives more control over on-screen displays and widgets.

OUTPUT=$(xrandr | grep | | awk '{print $1}') # Get display name!
INCR-.05 # For finer-grained control, set INCR to .03 or .02
old_brightness=$(xrandr --verbose | grep brightness | awk '{print $2}')

if [ -z "$1" ];
then
```

17. System and Administrative Commands
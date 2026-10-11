# JOB DEFINITION FILES IN `/etc/event.d`

As Fedora transitions from SysVinit to Upstart init, more jobs will be defined in the `/etc/event.d` directory. This section describes some of the jobs that the Upstart packages (page 418) put in this directory.

# SPECIFYING EVENTS WITH ARGUMENTS

The `telinit` and `shutdown` utilities emit *runlevel* events that include arguments. For example, `shutdown` emits *runlevel 0*, and `telinit 2` emits *runlevel 2*. You can match these events within a job definition using the following syntax:

```
start|stop on *event* [arg]
```

where *event* is an event such as *runlevel* and *arg* is an optional argument. To stop a job when the system enters *runlevel 2*, specify *stop on runlevel 2*. You can also specify *runlevel [235]* to match runlevels 2, 3, and 5 or *runlevel [!2]* to match any runlevel except 2.

Although Upstart ignores additional arguments in an event, additional arguments in an event name within a job definition file must exist in the event. For example, *runlevel* (no argument) in a job definition file matches all *runlevel* events (regardless of arguments), whereas *runlevel 5 arg2* does not match any *runlevel* event because the *runlevel* event takes only one argument.

The `/etc/event.d/rc2` job definition file defines the *rc2* task, which is similar to the other *rcn* tasks. The *rc2* task is started when the system enters *multiuser* mode without NFS (the event is named *runlevel 2*); it is stopped when the system enters any *runlevel* other than *runlevel 2* (*runlevel [!2]*). The first part of the script calls the *runlevel* utility (page 424), which makes the system appear to be in *runlevel 2* (there are no real runlevels) and assigns values to two variables. The real work is done by the *exec* command, which runs the `/etc/init.d/rc` script with an argument of 2. This script calls the links in the `/etc/rcn.d` directory that correspond to its argument. Thus the *rc2* task runs the init scripts that the links in the `/etc/rc2.d` directory point to.

```
$ cat /etc/event.d/rc2
# rc2 - runlevel 2 compatibility
#
# This task runs the old sysv-rc runlevel 2 ("multi-user") scripts. It
# is usually started by the telinit compatibility wrapper.
```

start on *runlevel 2*

stop on *runlevel [!2]*

console output

```
script
set $(runlevel --set 2 || true)
if [ "$1" != "unknown" ]; then
PREVLEVEL=$1
```
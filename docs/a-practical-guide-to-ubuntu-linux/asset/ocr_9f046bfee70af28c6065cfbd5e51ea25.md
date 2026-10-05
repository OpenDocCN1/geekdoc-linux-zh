# 442 CHAPTER 11 SYSTEM ADMINISTRATION: CORE CONCEPTS

only—it does not change the current state of any service. Give the following command to see the list of services:

```
$ sudo sysv-rc-conf --list
acpi-support 1:off 2:on 3:on 4:on 5:on
acpid
alisa-mixer-s
anacron
apparmor S:on
apport
atd
avahi-daemon
binfmt-suppo 2:on 3:on 4:on 5:on
bluetooth 0:off 1:off 2:on 3:on 4:on 5:on 6:off
...
```

All services that run their daemons are listed, one to one, followed by their configured state for each runlevel. If a runlevel is missing, it means there is no entry for the service in the /etc/rc.d directory. When all runlevels are missing, it means the service is controlled by Upstart. You can check how a specific daemon is configured by adding its name to the previous command:

```
$ sudo sysv-rc-conf --list cups
```

```
cups 1:off 2:on 3:on 4:on 5:on
```

# The name of the job/init script may differ from the name of the daemon it

> The following example shows that the ssh daemon. You can find the name of the job that controls a daemon by listing the contents of the /etc/init and /etc/init.d directories and searching for a filename that is similar to the name or function of the daemon you want to work with. For example, the /etc/init.d/cups script controls the printing daemon.

Frequently, the first few lines of a script or the comments the exec and desc stanzas of a job identify the daemon it controls. The following job description file shows these lines:

```
$ cat /etc/init/ssh.conf
# ssh OpenSSH Shell server
# The OpenSSH server provides secure shell access to the system.
...
description "OpenSSH server"
exec /usr/sbin/sshd
```

In the next example, sysv-rc-conf (sysv-rc-conf package) configures the /etc/rc.d directories so that the cupsd daemon is off in runlevels 2, 3, 4, and 5 and confirms the change. To make these kinds of changes, you must work with root privileges:

```
$ sudo sysv-rc-conf --level 2345 cups off
$ sudo sysv-rc-conf --list cups
cups 1:off 2:off 3:off 4:off 5:off
```
When a process is already running, you can change the process's nice value using the renice command. Here are some examples of the renice command.

Renice sarwar's processes +2:

```
$ renice +2 -u sarwar
$ 
Renice PID 2576 by +5
$ renice +5 2576
$
```

Renice sarwar's ksmserver processes to -3:

```
$ renice -3 `pgrep -u sarwar ksmserver`
2545: old priority -1, new priority -3
2546: old priority -1, new priority -3
2547: old priority -1, new priority -3
```

The back quotes are used in the previous command lines to indicate that the output of the pgrep command (presumably PIDs) be fed to the nice and renice command. The nice settings for your processes are displayed by default when you run top.

In PC-BSD, you can control kernel parameters with the system running using the sysctl command. You can also add parameters permanently to the /etc/sysctl.conf file, so they can load as a group or at each reboot. Some useful examples are as follows.

List all kernel parameters:

```
$ sysctl -a | less
kernel.ostype: FreeBSD
kernel.osrelease: 10.0-RELEASE-p12
kern.osrevision: 199506
kern.version: FreeBSD 10.0-RELEASE-p12 #0: Wed June 4 14:50:48 UTC 2014
... [Output truncated]
```

List the value of particular parameter:

```
$ sysctl kern.hostname
kern.hostname:
```

For our system, it was listed as pcbsd-4976.
Set the value of kernel.geom.debugflags to 16:

```
$ sysctl kern.geom.debugflags=16
```

If you want to change any of your kernel parameters permanently, you should add them to the /etc/sysctl.conf file. Parameter settings in that file are in the form parameter = value.
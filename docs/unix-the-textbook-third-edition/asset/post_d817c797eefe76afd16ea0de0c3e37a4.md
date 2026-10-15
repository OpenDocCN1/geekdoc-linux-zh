
# TABLE 23.8 Performance-Tuning Functions

| System Component | Control Facility |
|---|---|
| CPU | Nice numbers |
|  | Process priorities |
|  | Batch queues |
|  | Scheduler parameters |
| Memory | Process resource limits |
|  | Memory management parameters |
|  | Paging space |
| ZFS vdevs, zpools and I/O | ZFS pool and file system organization |
|  | ZFS deduplication, efficiency, optimization |
|  | I/O parameters |
| Network I/O | Network memory buffers |
|  | Network-related parameters |
|  | Network infrastructure |

The commands and configuration files that implement and affect some of the functions from Table 23.8 are

```
For PC-BSD- ps, sysctl, /etc/sysctl.conf
For Solaris- ps, dispadmin, ndd, /etc/system
```

## 23.8.1 Process and Memory Management

The most important, complete, and readily available display of system activity is given by the ps command. The following code example shows you the display of the nine top current processes using the most CPU resources running on the system. When we type this in on our PC-BSD system, we get the output shown:

```
[bob@pcbsd-4976] % ps aux | head -10
USER       PID %CPU %MEM    VSZ   RSS TT  STAT STARTED      TIME COMMAND
root         11 198.0  0.0      0    32  -  RL   Fri10PM   5437: [idle]
                                            07.08
root       6737   2.0  1.0 162592 61176  -  I<   Fri10PM   6:50.26 X :0 -auth
                                            /tmp/.
                                            PCDMA
bob       99659   1.8  0.1  23656  3948 1  Ss   2:51PM   0:00.15 /bin/csh
bob       99654   1.1  1.1 505084 66592  -   S    2:51PM   0:00.55 kdeinit4:
                                            kdeinit4:
                                            kk
bob       17229   0.8  2.6 1047556 157644 -  I    Fri10PM   1:01.80 kdeinit4:
                                            kdeinit4:
                                            pdt
root         0   0.0  0.1      0  4880  -  DLs   Fri10PM   5:52.47 [kernel]
root      1  0.0  0.0  9432   756 - SLs   Fri10PM 0:00.08 /sbin/init--
root      2  0.0  0.0    0    16 - DL    Fri10PM 0:00.00 [crypto]
root      3  0.0  0.0    0    16 - DL    Fri10PM 0:00.00 [crypto
returns]
[bob@pcbsd-4976] ~$
```

A similar output can be obtained in Solaris by giving the following command:

```
%ps -ef | head -10
```

The pgrep command displays the PIDs of running processes. Here are some examples of how to use pgrep to find the process IDs of the running processes and pipe those PIDs to another command to produce the output.

Search for kdeinit and run ps (assumes you are running the KDE4 desktop environment).

```
$ ps -p 'pgrep kdeinit'
PID   TT   STAT   TIME   COMMAND
17189 -   Is    00:00.96 kdeinit4: kdeinit4 Running...
(kdeinit4)
... [Output truncated]
$
```

Search for okular and run ps

```
$ ps -fp 'pgrep okular'
PID   TT STAT   TIME   COMMAND
46917 -  I    0:27:14 okular /usr/local/share/pcbsd/
doc/handbook_en.pdf
$
```

Search for okular, improve its priority (assumes Okular, the PDF viewer, is running and you are the superuser).

```
$ renice -1 'pgrep okular'
46917: old priority 0, new priority -1
$
```

The nice and renice commands, as seen in the previous example, change process priorities in the CPU.

Here is an example of using a command with nice to change a command's nice value.

Launch FileZilla at higher priority:

```
$ nice -n -1 filezilla
$
```

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

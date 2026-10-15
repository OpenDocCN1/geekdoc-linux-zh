# 11.8.1 Displaying the Host Name

Network-based applications use the user@host address format to identify a user on a network on the Internet. You can use the hostname and uname commands to display the name of the host you are logged on to. On some systems, the host name is shown in the short, simple name format, and on others it is displayed in the long, FQDN format. If you have to identify the host on the network that you are logged on to, you can use the hostname -s command to display the short format, which is simply the name of the host (the left-most string in the FQDN format). Some systems do not allow you to use the -s option unless you are the superuser. You can use the uname -n command to display the host name of the computer that you are logged on to in the FQDN format. The uname -a command displays complete information about a host, including the operating system it is running and the name of the CPU. On Solaris, you can use the -X option to display the expanded information, one item per line. The following are some examples of the hostname and uname commands on Solaris.

```
$ hostname
solarissrv
$ uname -n
solarissrv
$ uname -a
SunOS solarissrv 5.11 11.2 i86pc i386 i86pc
$ uname -X
System = SunOS
Node = solarissrv
Release = 5.11
KernelID = 11.2
Machine = i86pc
BusType = <unknown>
Serial = <unknown>
Users = <unknown>
OEM# = 0
Origin# = 1
NumCPU = 4
$
```

The following are the sample runs of hostname and uname on PC-BSD.

```
% hostname
pcbsd-srv
% uname -n
pcbsd-srv
% uname -a
FreeBSD pcbsd-srv 10.0-RELEASE-p6 FreeBSD 10.0-RELEASE-p6 #0
acf484b(releng/10.0) : Mon Feb 24 15:14:38 EST 2014 root@avenger:/usr/obj/root/pcbsd-build-10.0-EDGE/git/freebsd/sys/GENERIC amd64
%
```
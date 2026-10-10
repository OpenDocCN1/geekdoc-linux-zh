Class A address allows a client and server on the same host to communicate with one another via TCP/IP. A datagram sent to the loopback interface won't go out onto the network; it will simply go through the loopback.

The second line is for the default route. This entry says to send packets to Router 1 if a more specific route can't be found. In this case, the router has a UG under Flags. Some routers are configured with a U: others, such as the one in this example, with a UG. I've found that I usually end up determining through trial and error whether a U or UG is required. If there is a U in Flags and I am unable to ping a system on the other side of a router, a UG entry usually fixes the problem.

The third line is for the system's network interface, lo4b. This means to use this network interface for packets to be sent to 128.185.61.

# ## Checking Processes with ps

Knowing about the processes running on your system, and knowing how to stop them, are important to both system administration and performance.

To find the answer to “What is my system doing?”, use ps -ef. This command provides information about every running process on your system. If, for instance, you want to know whether NFS is running, you simply type ps -ef and look for NFS daemons. Although ps tells you every process that is running on your system, it doesn't provide a good summary of the level of system resources being consumed. I would guess that ps is the most often issued system administration command. There are a number of options you can use with ps. I normally use e and f, which provide information about every (“e”) running process and list this information in full (“f”). ps outputs are almost identical from system to system. The following three examples are from a Solaris, AIX, and HP-UX system, respectively:

Solaris example:

```
```text
martyn$ ps -ef
UID PR FPID PPID C STIME TTY TIME CMD
root 0 0 0 Feb 18 ? 0:01 sched
root 1 0 0 Feb 18 ? 1:30 /etc/init
root 2 0 0 Feb 18 ? 0:02 pagingd
root 3 0 1 Feb 18 ? 813:44 (aislush)
root 3063 3059 0 Feb 22 ? 0:10 /usr/dt/bin/hsperfclertner - -H r
root 88 1 0 Feb 18 ? 0:02 /usr/bin/in.nutd -g
root 478 0 Feb 18 ? 0:00 /usr/lib/saff/mnc - 300
root 94 0 0 Feb 18 ? 2:50 /usr/sbin/syslogd
root 150 1 0 Feb 18 ? 0:03 /usr/sbin/syslogd
root 96 1 0 Feb 18 ? 0:00 /usr/sbin/keyserv
```
```
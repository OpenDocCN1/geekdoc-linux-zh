
Implementations of ps have become hopelessly complex over the last decade. Several vendors have abandoned the attempt to define meaningful displays and made their pses completely configurable. With a little customization work, almost any desired output can be produced. As a case in point, the ps used by Linux is a trisexual and hermaphroditic version that understands multiple option sets and uses an environment variable to tell it what universe it’s living in.

Do not be alarmed by all this complexity: it’s there mainly for developers, not for system administrators. Although you will use ps frequently, you only need to know a few specific incantations.

![](img/14d78e3cecac4581d37024baf1e94cca_179_0.png)

On Linux and AIX, you can obtain a useful overview of all the processes running on the system with ps aux. The a option means to show all processes, x means to show even processes that don’t have a control terminal, and u selects the "user oriented" output format. Here’s an example of ps aux output on a machine running Red Hat (AIX output for the same command differs slightly):

```
redhat$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY   STAT TIME COMMAND
root         1  0.1  0.2  3356   560 ?    S    0:00 init [5]
root         2  0    0      0     0 ?    SN   0:00 [ksoftirqd/0]
root         3  0    0      0     0 ?    S<   0:00 [events/0]
root         4  0    0      0     0 ?    S<   0:00 [khelper]
root         5  0    0      0     0 ?    S<   0:00 [kacpid]
root        18  0    0      0     0 ?    S<   0:00 [kblockd/0]
root        28  0    0      0     0 ?    S    0:00 [pdfflush]
...
root       196  0    0      0     0 ?    S    0:00 [kjournald]
root      1050  0    0.1 2652   448 ?    Ss   0:00 udevd
root      1472  0    0.3 3048  1008 ?    Ss<  0:00 /sbin/dhclient -1
root      1646  0    0.3 3012  1012 ?    Ss<  0:00 /sbin/dhclient -1
root      1733  0    0      0     0 ?    S    0:00 [kjournald]
root      2124  0    0.3 3004  1008 ?    Ss   0:00 /sbin/dhclient -1
root      2182  0    0.2 2264   596 ?    Ss   0:00 syslogd -m 0
root      2186  0    0.1 2952   484 ?    Ss   0:00 klogd -x
rpc       2207  0    0.2 2824   580 ?    Ss   0:00 portmap
rpcuser   2227  0    0.2 2110   760 ?    Ss   0:00 rpc.statd
root      2260  0    0.4 5668  1084 ?    Ss   0:00 rpc.idmapd
root      2336  0    0.2 3268   556 ?    Ss   0:00 /usr/sbin/acpid
root      2348  0    0.8 9100  2108 ?    Ss   0:00 cupsd
root      2384  0    0.6 4080  1660 ?    Ss   0:00 /usr/sbin/sshd
root      2399  0    0.3 2780   828 ?    Ss   0:00 xinetd -stayalive
root      2419  0    1.1 7776  3004 ?    Ss   0:00 sendmail: accept
...
```

Command names in brackets are not really commands at all but rather kernel threads scheduled as processes. The meaning of each field is shown in Table 5.4 on the next page.

Another useful set of arguments for Linux and AIX is lax, which provides more technical information. The a and x options are as above (show every process), and

## Table 5.4 Explanation of ps aux output

| Field | Contents |
|-------|----------|
| USER | Username of the process's owner |
| PID | Process ID |
| %CPU | Percentage of the CPU this process is using |
| %MEM | Percentage of real memory this process is using |
| VSZ | Virtual size of the process |
| RSS | Resident set size (number of pages in memory) |
| TTY | Control terminal ID |
| STAT | Current process status:
R = Runnable        D = In uninterruptible sleep
S = Sleeping (< 20 sec) T = Traced or stopped
Z = Zombie
Additional flags:
W = Process is swapped out
< = Process has higher than normal priority
N = Process has lower than normal priority
L = Some pages are locked in core
s = Process is a session leader |
| TIME | CPU time the process has consumed |
| COMMAND | Command name and arguments* |

a. Programs can modify this info, so it's not necessarily an accurate representation of the actual command line.

l selects the "long" output format. ps lax is also slightly faster to run than ps aux because it doesn't have to translate every UID to a username—efficiency can be important if the system is already bogged down.

Shown here in an abbreviated example, ps lax includes fields such as the parent process ID (PPID), nice value (NI), and the type of resource on which the process is waiting (WCHAN).

```
redhat$ ps lax
F UID  PID  PPID PRI NI  VSZ   RSS WCHAN  STAT TIME COMMAND
4   0    1    0  16  0  3356  560  select S    0.00 init [5]
1   0    2    1  34 19    0    0 ksoftirqd/0 SN   0.00 [ksoftirqd/0]
1   0    3    1  5-10   0    0 worker S<   0.00 [events/0]
1   0    4    3  5-10   0    0 worker S<   0.00 [khelper]
5   0  2186  1  16  0  2952  484 syslog Ss   0.00 klogd -x
5  32  2207  1  15  0  2824  580 -     Ss   0.00 portmap
5  29  2227  1  18  0  2100  760 select Ss   0.00 rpc.statd
1   0  2260  1  16  0  5668 1084 -     Ss   0.00 rpc.idmapd
1   0  2336  1  21  0  3268  556 select Ss   0.00 acpid
5   0  2384  1  17  0  4080 1660 select Ss   0.00 sshd
1   0  2399  1  15  0  2780  828 select Ss   0.00 xinetd -sta
5   0  2419  1  16  0  7776 3004 select Ss   0.00 sendmail: a
...
```

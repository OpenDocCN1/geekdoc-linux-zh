
# $ netstat -rn

## Routing tables

| Destination | Gateway | Flags | Refs | Use | Interface | Pmtu |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 127.0.0.1 | 127.0.0.1 | UH | 0 | 28 | lo0 | 4608 |
| default | 128.185.61.1 | UG | 0 | 0 | lan0 | 4608 |
| 128.185.61 | 128.185.61.2 | U | 347 | 28668 | lan0 | 1500 |

![](img/75f39fc91296b889c0653851accdfd46_896_0.png)

With **netstat**, some information is provided about the router, which is the middle entry. The **-r** option shows information about routing, but there are many other useful options to this command are available. Of particular interest in this output is “Flags,” which defines the type of routing that takes place. Here are descriptions of the most common flags, which may be different among UNIX variants, from the manual page at the end of this chapter.

- 1=U Route to a *network* via a gateway that is the local host itself.
- 3=UG Route to a *network* via a gateway that is the remote host.
- 5=UH Route to a *host* via a gateway that is the local host itself.
- 7=UGH Route to a *host* via a remote gateway that is a host.

The first line is for the local host or loopback interface called **lo0** at address 127.0.0.1 (you can see this address in the **netstat -rn** example). The **UH** flags indicate that the destination address is the local host itself. This class A address allows a client and server on the same host to communicate with one another with TCP/IP. A datagram sent to the loopback interface won’t go out onto the network; it will simply go through the loopback.

The second line is for the default route. This entry says to send packets to router1 if a more specific route can’t be found. In this case, the router has a UG under Flags. Some routers are configured with a U; others, such as the one in this example, with a UG. I've found that I usually end up determining through trial and error whether a U or UG is required. If there is a U in flags and I am unable to ping a system on the other side of a router, a UG usually fixes the problem.

The third line is for the system's network interface `lan0`. This means to use this network interface for packets to be sent to 128.185.61.

## Check Processes with `ps`

![](img/75f39fc91296b889c0653851accdfd46_897_0.png)

![](img/75f39fc91296b889c0653851accdfd46_897_1.png)

Knowing about the processes running on your system, and knowing how to stop them, are important to both system administration and performance. Therefore, this process section, the `kill` command, and signals appear in both this chapter and the system administration chapter.

To find the answer to "What is my system doing?", use `ps -ef`. This command provides information about every running process on your system. If, for instance, you want to know whether NFS is running, you simply type `ps -ef` and look for NFS daemons. Although `ps` tells you every process that is running on your system, it doesn't provide a good summary of the level of system resources being consumed. I would guess that `ps` is the most often issued system administration command. There are a number of options you can use with `ps`. I normally use `e` and `f`, which provide information about every ("e") running process and lists this information in full ("f"). `ps` outputs are almost identical from system to system. The following three examples are from a Solaris, AIX, and HP-UX system, respectively:

Solaris example:

```
martyr $ ps -ef
    UID  PID  PPID C STIME TTY    TIME CMD
    root 0    0  0 Feb 18 ?  0:01 sched
    root 1    0  0 Feb 18 ?  1:30 /etc/init -
    root 2    0  0 Feb 18 ?  0:02 pageout
    root 3    0  1 Feb 18 ?  6:13:44 fsflush
    root 3065 3059 0 Feb 22 ?  5:10 /usr/dt/bin/sdtperfmeter -f -H -r
root      68     1  0  Feb 18 ?    0:01 /usr/sbin/in.routed -g
root     478     1  0  Feb 18 ?    0:00 /usr/lib/saf/sac -t 300
root      94     1  0  Feb 18 ?    2:50 /usr/sbin/rpcbind
root     150     1  0  Feb 18 ?    6:03 /usr/sbin/syslogd
root      96     1  0  Feb 18 ?    0:00 /usr/bin/keserver
root     144     1  0  Feb 18 ?   50:37 /usr/lib/autofs/automountd
root    1010     1  0  Apr 12 ?    0:00 /opt/perf/bin/bin/oidmon
root     106     1  0  Feb 18 ?    0:02 /usr/lib/netsvc/yp/ypbind -broad
root     156     1  0  Feb 18 ?    0:03 /usr/sbin/cron
root     176     1  0  Feb 18 ?    0:00 /usr/sbin/lpsched
root     129     1  0  Feb 18 ?    0:00 /usr/lib/nfs/lockd
daemon   130     1  0  Feb 18 ?    0:01 /usr/sbin/vold
root   14798     1  0  Mar 09 ?   31:10 /usr/sbin/nscd
root     133     1  0  Feb 18 ?    0:10 /usr/sbin/inetd -s
root     197     1  0  Feb 18 ?    0:00 /usr/lib/power/powerd
root     196     1  0  Feb 18 ?    0:35 /etc/opt/licensedes/lmgrd.ste -c /d
root     213     1  0  Feb 18 ?   4903:09 /usr/lib/nfs/statd
root     199  196  0  Feb 18 ?    0:03 suntelchd -T 4 -c /etc/optd
root     219     1  0  Feb 18 ?    0:08 /usr/lib/sendmail -bd -q15m
root     209     1  0  Feb 18 ?    0:05 /usr/sbin/utmpd
root     2935    266  0  Feb 22 ?   48:08 /usr/openwin/bin/Xsun :0 -nobannana
root   16795  16763 1  07:51:34 pts/4  0:00 ps -ef
root    2963    2954  0  Feb 22 ?    0:17 /usr/openwin/bin/fbconsole
root     479     1  0  Feb 18 console 0:00 /usr/lib/saf/tyimon -g -h -p sunc
root    10976     1  0  Jun 01 ?    0:00 /opt/perf/bin/ttd
root     7468     1  0  Feb 24 ?    0:13 /opt/perf/bin/dvalarmd
root      266     1  0  Feb 18 ?    0:00 /usr/bin/login-daemon
martyp 16763  16761 0  07:46:46 pts/4  0:01 -ksh
root    10995     1  0  Jun 01 ?    0:01 /opt/perf/bin/perflbd
root      484    478  0  Feb 18 ?    0:00 /usr/lib/saf/tyimon
root     458     1  0  Feb 18 ?   20:06 /usr/lib/snmp/snmpdxp -y -c /etc/f
root    16792   3059  0  07:50:37 ?   0:00 /usr/lib/dt/dtscreen -mode blank
root     471     1  0  Feb 18 ?    0:07 /usr/lib/dmi/dmigsmpsd
root     474     1  0  Feb 18 ?    0:00 /usr/lib/dmi/dmigsxmid -s
root     485    458  0  Feb 18 ?   739:44 miibisa -r -p 32874
root    2954    2936  0  Feb 22 ?    0:01 /bin/ksh /usr/dt/bin/Xsession
root    2936    266  0  Feb 22 ?    0:00 /usr/dt/bin/dtlogin-daemon
root    3061    3059  0  Feb 22 ?    1:32 dtwm
root    3058     1  0  Feb 22 pts/2  0:01 /usr/dt/bin/dtssession
root     712    133  0  Feb 18 ?    0:01 rpc.ttdbserverd
root   11001   11000  0  Feb 22 ?    0:01 <defunct>
root    2938     1  0  Feb 22 ?    0:00 /usr/openwin/bin/fbconsole -d :0
root    2999    2954  0  Feb 22 pts/2  0:16 /usr/dt/bin/sdt_shell -c     unt
root    3059    3002  0  Feb 22 pts/2  283:35 /usr/dt/bin/dtssession
root    3063    3059  0  Feb 22 ?    0:03 /usr/dt/bin/dthelpview -helpVolur
root    3099    3062  0  Feb 22 ?    0:13 /usr/dt/bin/dtfile -geometry +700
root   11000  10995  0  Jun 01 ?    0:02 /opt/perf/bin/aqdbserver -t alarm
root    3002    2999  0  Feb 22 pts/2  0:01 -ksh cc unset DT_DISPLAY
root     730    133  0  Feb 18 ?   1:37 rpc.rstatd
root    3062    3059  0  Feb 22 ?   2:17 /usr/dt/bin/dtlogin -geometry +700
root    3067     1  0  Feb 22 ?    0:00 /bin/ksh /usr/dt/bin/setvolcheckm
root    3000     1  0  Feb 22 ?    0:00 /usr/dt/bin/dsdm
root    3078    3067  0  Feb 22 ?    0:00 /bin/cat /tmp/.removable/notify0
root    10984     1  0  Jun 01 ?   12:42 /opt/perf/dce/bin/dced -b
root    16761    133  0  07:46:45 ?  0:00 in.telnetd
martyp $
```

AIX example:

```
martyp $ ps -aef

     UID      PID   PPID C  STIME           TTY  TIME  CMD
    root        1      0 0  Feb 24    -  5:07  /etc/init
    root     2208   15520 0  Feb 24    -  8:21  dtwm
    root     2664      1 0  Feb 24    -  0:00  /usr/dt/bin/dtlogin-daemon
    root     2882      1 0  Feb 24    - 158:41 /usr/sbin/syncd 60
    root     3376    2664 5  Feb 24    - 35:98:41 /usr/gpp/X11/bin/X -D /usr/lib/
    root     3624    2664 0  Feb 24    -  0:00  dtlogin <0>
    root     3950      1 6  Feb 24    - 55:50:30 /usr/lpp/perf/bin/l1bnd
    root     4144      1 0  Feb 24    -  0:00  /usr/lpp/perf/bin/aimdemon
    root     4490      1 0  Feb 24    -  0:48  /usr/lpp/perf/bin/perflbd
    root     4906      1 0  Feb 24    -  0:00  /usr/lib/errdemon
```

![](img/75f39fc91296b889c0653851accdfd46_898_0.png)

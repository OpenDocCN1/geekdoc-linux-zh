
## How Long Does It Take?

  You can use the **time** command to see a report of the amount of **time** your shell program takes to run. The output of **time** is different for many UNIX variants. You may want to view the manual page for **time** to see what output you can expect. A typical output of **time** when in **csh** is shown in Figure 11-5.

![](img/75f39fc91296b889c0653851accdfd46_775_0.png)

  Because some of the scripts you write may consume a substantial amount of system resources, you may want to consider investigating some of the job-control capabilities of the C shell. The simplest job control you can use is to run scripts in the background so that the priority of the script is low. By issuing the script name followed by the **&**, you will run the script in the background. If you run several scripts in the background, you can get the status of these by issuing the **jobs** command. This is a more advanced C shell topic, but depending on the level of complexity of scripts you write, you may want to look into job control.

## Manual Pages of Some Commands Used in Chapter 11

  There are no manual pages included for this chapter. The manual pages for commands used in this chapter appear in many other chapters, including:

- csh - Chapter 7
- ksh - Chapter 6
- **grep**, **awk**, **sed**, and other tools - Chapter 10

# CHAPTER 12

# Introduction to System Administration

## System Administration

  We have been dancing around system administration throughout this book. We have touched on a lot of system administration, such as listing and killing processes in the shell programming chapter, viewing available disk space, and so on. In this chapter, we'll look at many unintrosive system administration commands. By unintrosive, I mean commands that do not alter the setup of your system and commands that a user may typically run.

  Your system administrator is responsible for the setup and operation of your system; however, there are many aspects of system setup in which users may be interested. We'll cover many of the most commonly used commands related to system setup and how your system is running. As a user you may be interested in the way in which your system operates and administration-related commands. In addition, there are some commands directly related to the work you are performing, such as listing the processes you are running and how to kill them, that you can run as a user.

  At the end of the chapter, I also provide manual pages for many of the commands used in this chapter. Much of what takes place in system administration can only be covered at a cursory level in a user book, and the manual pages provide additional detail but still won’t make you a system administration expert.

  The examples in this chapter were performed on Solaris, HP-UX, AIX, and Linux systems; however, the commands and files are similar from one system to another, so you should be able to relate the information in this chapter to your UNIX variant.

  Most UNIX variants come with a system administration tool. This tool provides a menu-driven way of performing common system administration tasks such as managing the following: users and groups; disks and file systems; networking; printers; and so on. There is no widely used standard for such management tools, so they are different for each UNIX variant. These tools usually require superuser access to run, because the user has control over the most important and critical aspects of the system. Some of these tools allow users other than superuser to perform a subset of tasks as defined by superuser. I do not cover system administration tools, because they are peculiar to the UNIX variant on which they run and are used mostly by the system administrator. I’ll cover many of the files used by system administrators and some of the more commonly used unintrusive commands. Some of the following sections also appear in other chapters.

### Check Processes with ps

![](img/75f39fc91296b889c0653851accdfd46_779_0.png)

  To find the answer to “What is my system doing?,” use **ps -ef**. This command provides information about every running process on your system. If, for instance, you want to know whether NFS is running, you simply type **ps -ef** and look for NFS daemons. Although **ps** tells you every process that is running on your system, it doesn’t provide a good summary of the level of system resources being consumed. I would guess that **ps** is the most often issued system administration command. There are a number of options you can use with **ps**. I normally use **e** and **f**, which provide information about every ("e") running process and lists this information in full ("f"). **ps** outputs are almost identical going from system to system. The following three examples are from a Solaris, AIX, and HP-UX system, respectively:

Solaris example:

```
martyp $ ps -ef
      UID   PID  PPID  C     STIME TTY          TIME CMD
      root     0     0   0     Feb 18 ?           0:00 sched
      root     1     0   0     Feb 18 ?           1:30 /etc/init -
      root     2     0   0     Feb 18 ?           0:02 pageout
      root     3     0   1     Feb 18 ?           61:34 fssflush
      root  3065 3059  0 Feb 22 ?           5:10 /usr/dt/bin/sdtperformer -f -H -r
      root    88     1   0     Feb 18 ?           0:01 /usr/sbin/in.routed -q
      root   478     1   0     Feb 18 ?           0:00 /usr/lib/saf/sac -t 300
      root    94     1   0     Feb 18 ?           2:50 /usr/sbin/rcpid
      root   150     1   0     Feb 18 ?           6:03 /usr/sbin/syslogd
      root    96     1   0     Feb 18 ?           0:00 /usr/sbin/keyserv
      root   144     1   0     Feb 18 ?          50:37 /usr/lib/autofs/automountd
      root  1010    10   0     Apr 12 ?           0:00 /opt/bin/bin/ama daemon
      root   106     1   0     Feb 18 ?           0:02 /usr/lib/netsvc/yp/ypbind -broad
      root   156     1   0     Feb 18 ?           0:03 /usr/sbin/cron
      root   176     1   0     Feb 18 ?           0:00 /usr/lib/lpsched
      root   129     1   0     Feb 18 ?           0:00 /usr/lib/nfs/lockd
daemon   130     1   0     Feb 18 ?           0:01 /usr/sbin/nfs/lockd
      root 14798     1   0    Mar 09 ?          31:10 /usr/sbin/nscd
      root   133     1   0     Feb 18 ?           0:10 /usr/sbin/inetd -s
      root   197     1   0     Feb 18 ?           0:00 /usr/sbin/power/powerd
      root   196     1   0     Feb 18 ?           0:35 /etc/opt/ licenses/Imgrd.ste -c /d
      root   213     1   0     Feb 18 ?         4903:09 /usr/sbin/vold
      root   199   196   0     Feb 18 ?           0:03 suntecdh -T 4 -c /etc/opt/d
      root   219     1   0     Feb 18 ?           0:08 /usr/lib/sendmail -bd -q15m
      root   209     1   0     Feb 18 ?           0:05 /usr/lib/lp/ldap
      root   293   266   0     Feb 22 ?          48:08 /usr/openwin/bin/Xsun :0 -nobanner
      root 16795 16763  1   07:51:34 pts/4      0:00 ps -ef
      root  2963  2954  0     Feb 22 ?           0:17 /usr/openwin/bin/fbconsole
      root    79     1   0     Feb 18 ?           0:00 /usr/lib/saf/lttymon -g -h -p sunc
      root 10976     1   0    Jun 01 ?           0:00 /opt/perf/bin/ttd
      root  1468     1   0     Feb 24 ?           0:13 /opt/perf/bin/pvalarmd
      root   266     1   0     Feb 18 ?           0:01 /usr/dt/bin/dtlogin -daemon
martyp  1673 16761  1   07:46:46 pts/4      0:01 -ksh
      root 10995     1   0    Jun 01 ?           0:01 /opt/perf/bin/perflbd
      root   484   478   0     Feb 18 ?           0:00 /usr/bin/saf/ttymon
      root   458     1   0     Feb 18 ?          20:06 /usr/ib/snm/snmqxd -y -c /etc/f
      root  4791 3059  0   07:50:37 ?           0:00 /usr/dt/bin/dtscreen -mode blank
      root   471     1   0     Feb 18 ?           0:07 /usr/dt/dmi/dmispd
      root   474     1   0     Feb 18 ?           0:00 /usr/dt/dmi/snmpXdmid -s
      root   485   458   0     Feb 18 ?         739:44 mibiisa -r -P 32874
      root  2954  2936  0     Feb 22 ?           0:01 /bin/ksh /usr/dt/bin/Xsession
      root   236   266   0     Feb 22 ?           0:00 /usr/dt/bin/dtlogin -Xdaemon
      root  3061  3059  0     Feb 22 ?           1:32 dtwm
      root  3058     1   0  Feb 22 pts/2       0:01 /usr/dt/bin/dt/tsssession
      root   712   133   0     Feb 18 ?           0:01 rpc.ttdbserverd
      root 11001 11000  0     Feb 22 ?           0:01 <defunct>
      root  2938     1   0     Feb 22 ?           0:00 /usr/openwin/bin/fbconsole -d :0
      root  2999  2954  0     Feb 22 pts/2      0:16 /usr/dt/bin/sdt_shell -c
      root  3059 3002  0     Feb 22 pts/2       283:35 /usr/dt/bin/dt.dsession
      root  3063 3059  0     Feb 22 ?           0:03 /usr/dt/bin/dthelpview -help/olur
      root  3099  3062  0     Feb 22 ?           0:13 /usr/dt/bin/dtfile -geometry +700
      root 11000 10995  0    Jun 01 ?           0:02 /opt/perf/bin/agdbserver -t alar
      root  3002  2999  0     Feb 22 pts/2      0:01 -ksh -c                 unset DT;
      root   730   133   0     Feb 18 ?           1:37 rpc.statd
      root  3062  3059  0     Feb 22 ?           2:17 /usr/dt/bin/dtfile -geometry +700
      root  3067     1   0     Feb 22 ?           0:00 /usr/dt/usr/dt/bin/sdtvolcheckm
```

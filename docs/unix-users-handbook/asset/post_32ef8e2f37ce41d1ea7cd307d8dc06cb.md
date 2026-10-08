
# Check Processes with ps

8 S  root  2963  2954   0   40   20 f5f52028  513 f61b3l3e  Feb 22 ?  e
8 S  root     479     1   0  55  20 f5ee7120  407 f5de2c6  Feb 18 consolе  g
8 S  root   10976     1   0  65  20 f555828  478 f5c853е  Jun 01 ?  d
8 S  root    7468     1   0   46   20 f621d438  2851    8306c  Feb 24 ?  d
8 S  root     474     1   0  41  20 f5ee5520  1601 f5c6859е  Feb 18 ?  n
8 S  martyp  16763  16761   0  51  20 f6270140  429 f62701ac  07:46:46 pts/4  h
8 S  root   10995     1   0  40  20 f5b8f308  2350 f5fde56  Jun 01 ?  d
8 S  root     484   478   0  41  20 f5ee4e20  408 f5ee5048  Feb 18 ?  n
8 S  root     458     1   0  41  20 f5f54a18  504 f5fde906  Feb 18 ?  2m
80 0  root  16802  16763   1  61  20 f5ee7820    220  08:00:05 pts/4  l
8 S  root     471     1   0  41  20 f5f53c28  658 f5dfe726  Feb 18 ?  d
8 S  root     474     1   0  51  20 f5453528  804 f61a58b6  Feb 18 ?  g
8 S  root     485   458   0  40  20 f5f52e28  734 f607ecde  Feb 18 ?  74
8 S  root   2954  2936   0  40  20 f62e6540  433 f62e65ac  Feb 22 ?  n
8 S  root   2936   266   0  66  20 f5ee4720  1637 f5ee478c  Feb 22 ?  n
8 S  root   3061  3059   0  40  20 f5e17al8  2041 f61b359e  Feb 22 ?  m
8 S  root   3058     1   0  40  20 f61daa30  1067 f62aadс6  Feb 22 pts/2  n
8 S  root     712   133   0  41  20 f61d8e30   798 f61b390е  Feb 18 ?  d
8 Z  root  11001  11000   0  0 0 0        >
8 S  root     266     0   0  60  20 f5ee6320  513 f601bfb6  Feb 22 ?  0
8 S  root   2939  2954   0  40  20 f621e138  1450 f61b33bе  Feb 22 pts/2  t
8 S  root   3059  3002   1  51  20 f626d40  4010 f62aafa6  Feb 22 pts/2  2n
8 S  root   3063  3059   0  50  20 f62e8838  1952 f62aa556  Feb 22 ?  d
8 S  root   3099  3062   0  40  20 f5f52728  2275 f60a1dl8  Feb 22 ?  0
8 S  root  11000  10995   0  48  20 f6262740  2312   55694  Jun 01 ?  e
8 S  root   3002  2999   0  43  20 f61db8730  427 f61db89c  Feb 22 pts/2  =
8 S  root     730   133   0  40  20 f61d9530  422 f62aa9b6  Feb 18 ?  d
8 S  root   3062  3059   0  61  20 f61e7b38  2275 f62aa506  Feb 22 ?  0
8 S  root   3067     1   0  40  20 f5ee5c20  424 f5ee5c8с  Feb 22 ?  d
8 S  root   3000     1   0  40  20 f61d8030  518 f62aa8c6  Feb 22 ?  m
8 S  root   3078  3067   0  40  20 f61d9c30  211 f5b512b8  Feb 22 ?  0
8 S  root   10984     1   0  41  20 f5f54328  2484 ee4e684  Jun 01 ?  1b
8 S  root  16761   133   0  44  20 f5ee4020  411 f5c6894e  07:46:45 ?  d
martyp $

In this example, the first column is *F* for flags. *F* provides octal information about whether the process is swapped, in core, a system process, and so on. The octal value sometimes varies from system to system, so check the manual pages for your system to see the octal value of the flags.

*S* is for state. The state can be sleeping, as indicated by *S* for most of the processes shown in the example, waiting, running, intermediate, terminated, and so on. Again, some of these values may vary from system to system, so check your manual pages.

Some additional useful information in this output are: *NI* for the nice value; *ADDR* for the memory address of the process; *SZ* for the size in physical pages of the process; and *WCHAN*, which is the event for which the process is waiting.

# Killing a Process

If you issue the **ps** command and find that one of your processes is hung, or if you started a large job that you wish to stop, you can do so with the **kill** command. **kill** is a utility that sends a signal to the process you identify. You can **kill** any process that you own. In addition, superuser can **kill** almost any process on the system.

To **kill** a process that you own, simply issue the **kill** command and the Process ID (PID). The following example shows issuing the **ps** command to find all processes owned by *martyp*, **killing** a process, and checking to see that it has disappeared:

```
martyp $ ps -ef | grep martyp
 martyp 19336 19334 0 05:24:32 pts/4 0:01 -ksh
 martyp 19426 19336 0 06:01:01 pts/4 0:00 grep martyp
 martyp 19424 19336 5 06:00:48 pts/4 0:01 find / -name .login
martyp $ kill 19424
martyp $ ps -ef | grep martyp
 martyp 19336 19334 0 05:24:32 pts/4 0:01 -ksh
 martyp 19428 19336 1 06:01:17 pts/4 0:00 grep martyp
[1] + Terminated        find / -name .login &
martyp $
```

The example shows killing process *19424*, which is owned by *martyp*. We confirm that the process has indeed been killed by reissuing the **ps** command.

You can **kill** several processes on the command line by issuing **kill** followed by a space-separated list of all the process numbers you wish to **kill**.

Take special care when killing processes if you are logged in as superuser. You may adversely affect the way the system runs and have to manually restart processes or reboot the system.

# Signals

![](img/75f39fc91296b889c0653851accdfd46_904_0.png)

When you issue the kill command and process number, you are also sending a *signal* associated with the kill. We did not specify a *signal* in our kill example; however, the default *signal* of 15, or SIGTERM, was used. These *signals* are used by the system to communicate with processes. The *signal* of 15 we used to terminate our process is a soft-ware termination *signal* that is usually enough to terminate a user process such as the find we had started. A process that is difficult to kill may require the SIGKILL, or 9 *signal*. This *signal* causes an immediate termination of the process. I use this only as a last resort because processes killed with SIGKILL do not always terminate smoothly. To kill such processes as the shell, you sometimes have to use SIGKILL.

![](img/75f39fc91296b889c0653851accdfd46_904_1.png)

You can use either the *signal* name or number. These signal numbers sometimes vary from system to system, so view the manual page for *signal*, usually in section 5, to see the list of *signals* on your system. A list of some of the most frequently used *signal* numbers and corresponding *signals* follows:

| Signal number | Signal |
| :--- | :--- |
| 1 | SIGHUP |
| 2 | SIGINT |
| 3 | SIGQUIT |
| 9 | SIGKILL |
| 15 | SIGTERM |
| 24 | SIGSTOP |

To kill a process with id 234 with SIGKILL, you would issue the following command:

```
$ kill -9 234
```
- kill command to terminate the process
- signal number
- process id (PID)

![](img/75f39fc91296b889c0653851accdfd46_905_0.png)

# Show Remote Mounts with showmount

showmount is used to show all remote systems (clients) that have mounted a local file system. showmount is useful for determining the file systems that are most often mounted by clients with NFS. The output of showmount is particularly easy to read because it lists the host name and the directory that was mounted by the client.

NFS servers often end up serving many NFS clients that were not originally intended to be served. This situation ends up consuming additional UNIX system resources on the NFS server, as well as additional network bandwidth. Keep in mind that any data transferred from an NFS server to an NFS client consumes network bandwidth, and in some cases may be a substantial amount of bandwidth if large files or applications are being transferred from the NFS server to the client. The following example is a partial output of showmount taken from a system. showmount runs on the HP-UX, AIX, and Linux systems I have been using throughout this chapter, but not the Solaris system:

```
# showmount -a
sys100.ct.mp.com//applic
sys101.ct.mp.com//applic
sys102.cal.mp.com//applic
sys103.cal.mp.com//applic
sys104.cal.mp.com//applic
sys105.cal.mp.com//applic
sys106.cal.mp.com//applic
sys107.cal.mp.com//applic
sys108.cal.mp.com//applic
sys109.cal.mp.com//applic
```

```
# showmount -a

sys200.cal.mp.com:/usr/users
sys201.cal.mp.com:/usr/users
sys202.cal.mp.com:/usr/users
sys203.cal.mp.com:/usr/users
sys204.cal.mp.com:/usr/users
sys205.cal.mp.com:/usr/users
sys206.cal.mp.com:/usr/users
sys207.cal.mp.com:/usr/users
sys208.cal.mp.com:/usr/users
sys209.cal.mp.com:/usr/users
```

The three following options are available to the **showmount** command:

- -**a** prints output in the format “name:directory,” as shown above.
- -**d** lists all the local directories that have been remotely mounted by clients.
- -**e** prints a list of exported file systems.

The following are examples of **showmount -d** and **-e**:

```
# showmount -d

/applic
/usr/users
/usr/oracle
/usr/users/emp.data
/network/database
/network/users
```

![](img/75f39fc91296b889c0653851accdfd46_906_0.png)

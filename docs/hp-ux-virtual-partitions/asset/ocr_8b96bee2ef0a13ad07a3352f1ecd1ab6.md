# System Startup and Shutdown Scripts

```
/sbin/init /dev/sys/tty /dev/syscons> /dev/console 2>kl

ccprt: bootwait:/sbin/cat /etc/copyright ./dev/syscons # legal req
sysrc: wait:/sbin/rc </dev/console >/dev/console 2>1 # system init
#post: powerwait:/sbin/powerfail /dev/console 2>1 # powerfail
conn: 123456:respawn:/usr/sbin/getty console console # system console
#tp1:234:respawn:/usr/sbin/getty -h ttyOpl 9600
#tp2:234:respawn:/usr/sbin/getty -h ttyOp2 9600
#tp3:234:respawn:/usr/sbin/getty -h ttyOp3 9600
#tp4:234:respawn:/usr/sbin/getty -h ttyOp4 9600
#tp5:234:respawn:/usr/sbin/getty -h ttyOp5 9600
#ups: respawn:/tmp/l 8 /usr/lib/upd_wond -f /etc/ups_conf
```

The **/sbin/rc** line is always present in the **/etc/initab** file. There is more information about **/etc/initab** coming shortly.

If you are booting your system to run level 3, then **/sbin/rc** will run the startup scripts present in **/sbin/rc1.d**, **/sbin/rc2.d**, and **/sbin/rc3.d**.

I have mentioned run levels several times in this discussion. Both the startup and shutdown scripts described here, as well as the **/etc/initab** file, depend on run levels. In HP-UX 11.x, the following run levels exist:

| 0 | Halted run level. |
| s | Run level s, also known as single-user mode, is used to ensure that no one else is on the system so you can proceed with system administration tasks. |
| 1 | Run level 1 starts various basic processes. |
| 2 | Run level 2 allows users to access the system. This is also known as multi-user mode. |
| 3 | Run level 3 is for exporting NFS file systems. |
| 4 | Run level 4 starts the graphical manager, including HP Common Desktop Environment (HP CDE). |
| 5 and 6 | Not currently used. |

**/etc/initab** is also used to define a variety of processes that will be run, and it is used by **/sbin/init**. The **/sbin/init** process ID is 1. It is the first process started on your system and has no parent. The **init** process looks at / **etc/initab** to determine the run level of the system.
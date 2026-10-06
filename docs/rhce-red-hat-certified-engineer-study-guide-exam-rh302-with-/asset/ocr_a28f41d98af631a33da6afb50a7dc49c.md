# TABLE 15.7 Actions Specifiable in /etc/inittab (continued)

| Action | Description |
| --- | --- |
| once | The process is executed once when the specified runlevel is entered. |
| demand | The process is executed whenever the specified runlevel (a, b or c) is called. However, no runlevel change will occur. |
| powerfail | The process is executed when the power goes down. The init process will not wait for the process to finish. |
| powerfail | This process is executed when init is told that the battery of the external Uninterrupted Power Supply (UPS) is almost exhausted. |
| powerokwa | This process is executed when init is informed that the power has been restored. |
| powerwait | The process is executed when the power goes down. The init process will wait for the process to finish. |
| respawn | The process is restarted whenever it terminates. |
| sysinit | The process is executed during system boot, before any boot entries. The runlevel field is ignored. |
| wait | The process is executed when the specified runlevel is entered; init will wait for its termination. |

Here are the contents of a typical /etc/inittab file:

id:3:initdefault:

si::sysinit:/etc/rc.d/rc.sysinit

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

Copyright ©2000 SYBEX, Inc., Alameda, CA    www.sysex.com
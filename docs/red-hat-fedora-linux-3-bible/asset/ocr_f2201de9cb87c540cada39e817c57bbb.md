> **TIP**: I recommend posting your failed PPP output to the comp.protcol.ppp newsgroup, where some very smart PPP experts can help answer your questions. Before you post, however, read a few days' worth of messages from the group. Chances are that someone has already run into the same problem and has a solution. Also, post only the parts of the log file that are relevant. You can also ask your local Linux user group for help.

To have debugging directed to a separate log file for PPP, add these lines to the `/etc/syslog.conf` file:

```
```
daemon.*      /var/log/pppmsg
local2.*      /var/log/pppmsg
```
```

After this, restart the syslog daemon process as follows:

```
```
# service syslog restart
```
```

It's best to try to do this debugging process from the desktop because it helps to have several Terminal windows open (I would suggest at least three). From the first window, start a command that lists the contents of the log file we just defined above (pppmsg) as debug messages come in:

```
```
# tail -f /var/log/pppmsg
```
```

In the next window, start the PPP interface. Assuming it is the ppp0 interface, use the following command as root user:

```
```
# ifup ppp0
```
```

Here is a partial listing of the output:

```
```
Sep  6 20:43:51 maple pppd[2077]: pppd 2.4.1 started by root, uid 0
Sep  6 20:43:51 maple ifup-ppp: pppd started for ppp0 on /dev/modem at 115200
Sep  6 20:43:52 maple chat[2079]: abort on (BUSY)
Sep  6 20:43:52 maple chat[2079]: abort on (ERROR)
Sep  6 20:43:52 maple chat[2079]: abort on (NO CARRIER)
Sep  6 20:43:52 maple chat[2079]: abort on (NO DIALTONE)
Sep  6 20:43:52 maple chat[2079]: abort on (Invalid Login)
Sep  6 20:43:52 maple chat[2079]: abort on (Login incorrect)
Sep  6 20:43:52 maple chat[2079]: send (ATE)
Sep  6 20:43:52 maple chat[2079]: expect (OK)
Sep  6 20:43:53 maple chat[2079]: AT:"
Sep  6 20:43:53 maple chat[2079]: OK
Sep  6 20:43:53 maple chat[2079]: -- got it
Sep  6 20:43:53 maple chat[2079]: send (ATDT5551212")
Sep  6 20:44:10 maple chat[2079]: expect (CONNECT)
Sep  6 20:44:10 maple chat[2079]: "
Sep  6 20:44:10 maple chat[2079]: ATDT5551212"
Sep  6 20:44:10 maple chat[2079]: CONNECT
Sep  6 20:44:10 maple chat[2079]: -- got it
Sep  6 20:44:10 maple chat[2079]: send (\d)
```
```
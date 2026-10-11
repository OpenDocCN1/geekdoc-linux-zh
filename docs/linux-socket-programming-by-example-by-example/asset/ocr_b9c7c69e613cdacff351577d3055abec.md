```
Enter format string: %x %x
Result from 127.7.7.7 port 9090 :
'11/09/99 19:11:32
Enter format string: CTRL+D
$
```

If you did this quickly enough, the server should have been able to process both of these requests within one single server process. To see whether this worked, check the server log:

```
$ tail -f /tmp/dgramisrvr.log
[PID 1279] dgramisrvr started.
[PID 1279] Got request '%A %B %D' from 127.7.7.7 port 1027
[PID 1279] Timed out: server exiting.
[PID 1294] dgramisrvr started.
[PID 1294] Got request '%x' from 127.7.7.7 port 1027
[PID 1294] Got request '%x %x' from 127.7.7.7 port 1027
[PID 1294] Timed out: server exiting.
```

The last four log lines confirm that server process ID 1294 was able to process both date requests before it timed out.

# Uninstalling the Demonstration Programs

To uninstall the demonstration programs, perform the following:

```
$ make clobber
rm -f *.o core a.out
rm -f /tmp/wrapper.log /tmp/dgramisrvr.log
rm -f /tmp/inetd.conf /tmp/wrapper /tmp/dgramisrvr
rm -f dgramisrvr wrapper dgramisrvr2
student1 12763 1 0 23:04 ? 00:00:00 /usr/sbin/inetd /tmp/inetd.conf
```

If you see your inetd process running above, you may want to kill it now.

```
$
```

The clobber target of the Makefile provided will remove all of the files created in the /tmp directory and attempt to display the process ID of your inetd daemon. In the example output shown, the daemon is running as PID 12763. This should be terminated with the kill command as follows:

```
$ kill 12763
$
```
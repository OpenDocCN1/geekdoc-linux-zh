```
::
*)
echo "Usage: $0 {start|stop|reload|restart}"
exit 1
esac
test "$return" = '$rc_done' || exit 1
exit 0
```

Note that the S20rwhod script can be used to start and kill the rwhod daemon, since it checks for the command-line argument with which it was called.

The first time that you boot up your system, make sure to record which daemons get started to ensure that you are not running anything that you don't intend to run. The trusty `ps` command is the right tool to verify which `/etc/rc.d` services are running on your server, as shown in Listing 4.6.

# Listing 4.6 Looking for active network services in the process table

```
[root]$ ps aux
root 1 0.0 0.0 400 280 ? S 15:02 0:03 init
root 2 0.0 0.0 0 0 ? SW 15:02 0:00 [powerd]
root 3 0.0 0.0 0 0 ? SW 15:02 0:00 [kflushd]
root 4 0.0 0.0 0 0 ? SW 15:02 0:00 [kupdated]
root 5 0.0 0.0 0 0 ? SW 15:02 0:00 [kpiod]
root 6 0.0 0.0 0 0 ? SW 15:02 0:00 [kswapd]
root 7 0.0 0.0 0 0 ? SW 15:03 0:00 [md_thread]
root 86 0.0 0.2 1384 808 ? S 15:03 0:00 /usr/sbin/syslogd
root 190 0.0 0.2 1632 1064 ? S 15:03 0:00 /usr/sbin/klogd -c 1
root 270 0.0 0.6 7264 2336 ? S 15:03 0:00 /usr/sbin/httpd -f /etc/httpd/httpd.conf -D SUSEHELP
root 292 0.0 0.1 1280 648 ? S 15:03 0:00 /usr/sbin/gpm -t sun3 -m /dev/mouse
root 301 0.0 0.1 1344 704 ? S 15:03 0:00 /usr/sbin/inetd
root 341 0.0 0.4 2632 1600 ? S 15:03 0:00 sendmail: accepting connections
root 343 0.1 0.3 2376 1184 ? S 15:03 0:11 /usr/local/sbin/sshd
root 352 0.0 0.2 1552 880 ? S 15:03 0:00 /usr/sbin/cron
root 388 0.0 0.1 1224 632 tty2 S 15:03 0:00 /sbin/mingetty tty2
root 399 0.0 0.1 1224 632 tty3 S 15:03 0:00 /sbin/mingetty tty3
root 400 0.0 0.1 1224 632 tty4 S 15:03 0:00 /sbin/mingetty tty4
root 01 0.0 0.1 1224 632 tty5 S 15:03 0:00 /sbin/mingetty tty5
root 402 0.0 0.1 1224 632 tty6 S 15:03 0:00 /sbin/mingetty tty6
root 420 1.0 2.0 14144 7848 ? SL 15:03 1:57 /usr/X11R6/bin/X :0
```
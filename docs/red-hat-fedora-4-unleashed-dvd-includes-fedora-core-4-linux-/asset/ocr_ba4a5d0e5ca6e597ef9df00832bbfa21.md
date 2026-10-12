The locations of symbolic links can also be confusing. Red Hat (and now Fedora Core) has traditionally kept them in one place, and the Linux Standards Base (LSB) requires that they now be located elsewhere. Because other scripts reference these files and it would be difficult to change them all, Fedora Core places symbolic links in the places specified by the LSB.

As you might surmise, symbolic links are very powerful tools in the system administrator's toolbox.

# ## Understanding init Scripts and the Final Stage of Initialization

Each `/etc/rc.d/init.d` script, or *init* script, contains logic that determines what to do when receiving a start or stop value. The logic might be a simple switch statement for execution, as in this example:

```
case "$1" in
start)
start
;;
stop)
stop
;;
restart)
restart
;;
reload)
reload
;;
status)
rhstatus
;;
condrestart)
[ -f /var/lock/subsys/smb ] && restart || :
;;
*)
echo "$"Usage: $0 {start|stop|restart|status|condrestart}"
exit 1
esac
```

Although the scripts can be used to customize the way that the system runs from power-on, absent the replacement of the kernel, this script approach also means that the system does not have to be halted in total to start, stop, upgrade, or install new services.

Note that not all scripts will use this approach, and that other messages might be passed to the service script, such as restart, reload, or status. Also, not all scripts will respond to the same set of messages (with the exception of start and stop, which they all have to accept by convention) because each service might require special commands.
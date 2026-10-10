```
# description: Carpald is a program which wakes up every 60 minutes and
tells us that we need to take a break from the keyboard
# or we'll lose all functionality of our wrists and never
# be able to type again as long as we live.
#
# processname: carpald

# Source function library.
. /etc/rc.d/init.d/functions

[ -f /usr/local/sbin/carpald ] || exit 0

# See how we were called.
case "$1" in
start)
echo -n "Starting carpald: "
daemon carpald

echo
touch /var/lock/subsys/carpald
;;
stop)
echo -n "Stopping carpald services: "
killproc carpald

echo
rm -f /var/lock/subsys/carpald
;;
status)
status carpald
;;
restart|reload)
$0 stop
$0 start
;;
*)
echo "Usage: carpald [start|stop|status|restart|reload]"
exit 1
esac

exit 0
```
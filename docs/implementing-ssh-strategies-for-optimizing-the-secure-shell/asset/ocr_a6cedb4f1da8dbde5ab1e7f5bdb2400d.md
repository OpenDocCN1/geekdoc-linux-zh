```
PATH=/usr/local/sbin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/bin/X11/:
#
# required commands...
#

PPPD=/usr/sbin/pppd
SSH=/usr/bin/ssh

if ! test -f $PPPD ; then echo "can't find $PPPD"; exit 3; fi
if ! test -f $SSH ; then echo "can't find $SSH"; exit 4; fi

case "$1" in
start)
	# echo -n "Starting vpn to $SERVER_HOSTNAME: "
	$($PPPD) udetach noauth passive pty "$($SSH) $LOCAL_SSH_OPTS)
	$(SERVER_HOSTNAME) -l $(SERVER_USERNAME) -o Batchmode=yes sudo $(PPPD)
	nodetach notary noauth" ipparam vpn $(CLIENT_lFIPADDR):$(SERVER_IFIPADDR)
	# echo "connected."
	;;

stop)
	# echo -n "Stopping vpn to $SERVER_HOSTNAME: "
	PID=$(ps ax | grep "$($SSH) $(LOCAL_SSH_OPTS) $(SERVER_HOSTNAME) -
	l$(SERVER_USERNAME) -o" | grep -v ' passive ' | grep -v 'grep ' | awk
	' (print $1)')
	if [ "$(PID)" != "" ]; then
	kill $PID
	echo "disconnected."
	else
	echo "Failed to find PID for the connection"
	fi
	;;

config)
	echo "SERVER_HOSTNAME=$SERVER_HOSTNAME"
	echo "SERVER_USERNAME=$SERVER_USERNAME"
	echo "SERVER_IFIPADDR=$SERVER_IFIPADDR"
	echo "CLIENT_IFIPADDR=$CLIENT_IFIPADDR"
	;;

*)
	echo "Usage: vpn (start|stop|config)"
	exit 1
	;;
esac

exit 0
```
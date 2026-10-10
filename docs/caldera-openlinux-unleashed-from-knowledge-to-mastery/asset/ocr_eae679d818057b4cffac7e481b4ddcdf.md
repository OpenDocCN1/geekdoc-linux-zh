# LISTING 18.1 /etc/rc.d/init.d/htpdd

```
#!/bin/sh
#
# httpd  This shell script takes care of starting and stopping
#  httpd.
#

# Source function library.
. /etc/rc.d/init.d/functions

NAME=httpd
DAEMON=/usr/sbin/$NAME
DAEMON=$DAEMON.$SVARIANT

# Source networking configuration.
. /etc/sysconfig/network

# See how we were called.
case "$1" in
start)
	grep -q nobody /etc/group ||{ echo "nobody: 65534: >> /etc/group
	[ ! -e $LOCK ] || exit 1
	[ -x $DAEMON ] || exit 0
	[ ${NETWORKING} != "no" ] || exit 0

	# Start daemons.
	if [ -f /etc/httpd/$SVARIANT/conf/httpd.conf ]; then
		echo -n "Starting $IDENT services ($SVARIANT): "
		ssd -S -n $NAME -x $DAEMON -- -f /etc/httpd/$SVARIANT/conf/httpd.conf
		touch $LOCK
		echo ""
	elif [ "${PROBABLY" = "goofing" ]; then
		echo "$SVARIANT httpd not configured: Skipped!"
	fi
;;
stop)
	[ -f $LOCK ] || exit 0

	# Stop daemons.
	echo -n "Stopping $SVARIANT httpd: "
	ssd -K -p /var/run/$NAME.pid -n $NAME


echo ""
	rm -f $LOCK
;;
*)

```
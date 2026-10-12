```
RETVAL=$?
	echo
	KIND="NMB"
	echo -n "$Shutting down $KIND services: 	ikillproc nmbd
	RETVAL2=$?
	[ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && rm -f /var/lock/subsys/smb
	echo ""
	return $RETVAL
}

restart() {
	stop
	start
}

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
	*)
		echo "$Usage: $0 (start|stop|restart|status|condrestart)"
		exit 1
esac
exit $?
```

To illustrate what this script essentially does, I skipped some of the beginning of the script (where it checked if the network was up and running and set some values). Here are the actions **smb** takes when it is run with **start** or **stop**:

+   * **start** — This part of the script starts the **smbd** and **nmbd** servers when the script is run with the **start** option.
+   * **stop** — When run with the **stop** option, the `/etc/init.d/smb` script stops the **smbd** and **nmbd** servers.

The **restart** option runs the script with a **stop** option followed by a **start** option. If you wanted to start the **smb** service yourself, you could type the following command (as **root** user):

```
# /etc/init.d/smb start
Starting SMB services:				[   OK   ]
```
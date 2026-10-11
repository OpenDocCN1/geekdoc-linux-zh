```
exit
fi

killproc() {                # kill the named process(es)
pid=`/usr/bin/ps -e |\n        /usr/bin/grep -w $1 |\n        /usr/bin/sed -e 's/^ *//' -e 's/ .*//'`
[ "\$pid" != "" ] && kill \$pid
}

# Start/stop processes required for Samba server

case "$1" in
'start')
#
# Edit these lines to suit your installation (paths, workgroup, host)
#
echo Starting SMBD
/usr/local/samba/bin/smbd -D -s \\
/usr/local/samba/smb.conf

echo Starting NMDB
/usr/local/samba/bin/nmbd -D -l \\
/usr/local/samba/var/log -s /usr/local/samba/smb.conf

echo Starting Winbind Daemon
/usr/local/samba/sbin/winbindd
;;
'stop')
killproc nmbd
killproc smbd
killproc winbindd
;;
*)
	echo "Usage: /etc/init.d/samba.server { start | stop }"
;;
esac
```

Again, if you would like to run Samba in dual daemon mode, replace:

```
/usr/local/samba/sbin/winbindd
```
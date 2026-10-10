option, and possibly a restart option. For example, the following lines are part of the contents of the smb script that defines what happens when the script is run with different options to start or stop the Samba file and print service:

```
#!/bin/sh
#
# chkconfig: - 91 35
# description: Starts and stops the Samba smbd daemon \\
#             used to provide SMB network services.



start() {
KIND="SMB"
echo -n "Starting $KIND services: "
daemon smbd $SMBOPTIONS
RETVAL=$?
echo
[ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && touch /var/lock/
subs/smb || \\
RETVAL=1
return $RETVAL
}
stop() {
KIND="SMB"
echo -n "Shutting down $KIND services: "
killproc smbd
RETVAL=$?
echo
[ $RETVAL -eq 0 -a $RETVAL2 -eq 0 ] && rm -f /var/lock/
subs/smb
return $RETVAL
}
restart() {
stop
start
}
.
.
.
```

To illustrate the essence of what this script does, I skipped some of the beginning and end of the script (where it checked if the network was up and running and set some values). Here are the actions smb takes when it is run with start or stop:
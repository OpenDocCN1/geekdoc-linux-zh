> Don't be concerned if you see several instances of smbd. This occurrence is normal if several clients are connected to Samba shares.

Because both smb and nmb appear in this output, it's clear that both daemons are running independently. How do you get to this state, though?

Many Linux distributions, including Red Hat Linux 6.0, start the Samba daemons in the script /etc/rc.d/init.d/smb, which takes the parameters start, stop, restart, and status. So if Samba isn't already running, you can type /etc/rc.d/init.d/smb start to start it. The initialization scripts run the smb script at system startup, so after you install Samba and reboot, it should be running.

> If you've installed Samba and rebooted but it's not running, check for the presence of links called smb in /etc/rc.d/init.d and /etc/rc.d/rc5.d to /etc/rc.d/init.d/smb. If there are no such links, create them by typing ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc3.d and ln -s /etc/rc.d/init.d/smb /etc/rc.d/rc5.d

On some Linux distributions, you might need to start Samba by editing some other initialization script, such as /etc/rc.d/rc.local. You can add lines such as these to whatever startup script is convenient:

```
/usr/sbin/smbd -D
/usr/sbin/nmbd -D
```

You can also enter these lines directly at a command prompt if you want to start Samba manually. Running Samba independently in this way has the advantage that it can respond quickly to incoming requests. In my experience, this method is also somewhat more reliable than running Samba from inetd. Running Samba independently does, however, consume memory even when Samba isn't serving any clients.
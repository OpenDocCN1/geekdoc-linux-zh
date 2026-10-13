# Tip

When you use a delayed shutdown command, such as the one just described, users who are logged in see the warning message it broadcasts, but the shutdown does not prevent anyone from logging in during the shutdown countdown period. To disallow new logins, you can create a text file called /etc/nologin with an appropriate message stating that a shutdown has already been scheduled and that users should try to log in at a later time. Do not forget to rename or delete the file after you reboot.

# Caution

If you are remotely rebooting a server, be absolutely sure to remove or rename this file prior to the actual shutdown. No normal user accounts are allowed to log in when this file is present. In fact, you might want to add rm -f /etc/nologin at the end of the /etc/rc.local script and make sure that it is run by init at the end of run level 3.

To reboot immediately, you can run the following command as the superuser:

```
shutdown -r now
```

# Rebooting using Ctrl+Alt+Delete

If you are on the system console, you can use the traditional Ctrl+Alt+Delete key combination to reboot your server. The following line in /etc/inittab makes this possible:

```
ca::ctrlaltdel:/sbin/shutdown -t3 -r now
```

This line allows init to trap the Ctrl+Alt+Delete key combination and call the shutdown script to reboot immediately.

# Caution

Anyone who has physical access to your system console can shut down the system by pressing the Ctrl+Alt+Delete key combination. To protect yourself from such a shutdown, you can create a file called /etc/shutdown.allow that will contain a list of users (one username per line) who are allowed to shut down the system. The root account does not need to be listed in this file.
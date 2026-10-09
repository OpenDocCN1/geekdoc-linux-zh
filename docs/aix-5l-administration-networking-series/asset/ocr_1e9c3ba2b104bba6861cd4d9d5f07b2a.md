+   If you have applications that you want to always stop before a system shutdown or reboot, put the commands or script name in the `/etc/rc.shutdown` file.

+   To restart the system immediately after shutdown, shut the system down with the `shutdown -r` command or `reboot`.

+   If you suspect hardware problems or the system won’t boot, use the pSeries or RS/6000 diagnostic programs using the `diag` command to assist in determining the failure.
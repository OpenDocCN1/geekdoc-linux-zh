# 2.3. Use the timedatectl command to verify that the time zone is successfully set to America/Jamaica.

```
[student@server ~]$ timedatectl
Local time: Tue 2019-02-19 11:12:46 EST
Universal time: Tue 2019-02-19 16:12:46 UTC
RTC time: Tue 2019-02-19 16:12:46
Time zone: America/Jamaica (EST, -0500)
System clock synchronized: yes
NTP service: active
RTC in local TZ: no
```

# 3. Display all the log events in the previous 30 minutes from the current time on current server.

3.1. Use the date command to determine the time frame for which you want to view the journal entries.

```
[student@server ~]$ date
Feb 22 07:31:05 EST 2019
[student@server ~]$ date -d "-30 minutes"
Feb 22 07:01:35 EST 2019
```

3.2. Use the --since and --until units with the journalctl command to display all log events recorded in the previous 30 minutes on server. To journalctl Q

```
[student@server ~]$ journalctl --since 07:01:00 --until 07:31:00
...output omitted...
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Reached target Timers.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Reached target Paths.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Starting D-Bus User Session Bus.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Listening on D-Bus User Socket.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Reached target Sockets.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Reached target Basic.
Feb 22 07:24:28 server.lab.example.com systemd[1138]: Reached target Default.
Feb 22 07:24:28 server.lab.example.com systemd[1139]: Startup finished in 123ms.
Feb 22 07:24:28 server.lab.example.com systemd[1]: Started User Manager for UID 1000.
Feb 22 07:24:28 server.lab.example.com sshd[1134]: pam_unix(session): session opened for user student (uid=0)
Feb 22 07:26:56 server.lab.example.com systemd[1138]: Mark boot as successful.
Feb 22 07:26:56 server.lab.example.com systemd[1138]: Started Mark boot as successful.
lines 1-36 (END) q
[student@server ~]$
```

# 4. Create the /etc/rsyslog.d/auth-errors.conf with the necessary lines to help thesyslog service write messages related to authentication and security issues to the
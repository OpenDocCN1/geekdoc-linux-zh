
# Analyzing and Sorting Logs

[sudo] password for student: student

2.3. Use the timedatectl command to verify that the time zone has been updated to America/Port-au-Prince.

```
[student@server-a ~]$ timedatectl
Local time: Tue 2019-02-19 01:16:29 EST
Universal time: Tue 2019-02-19 06:16:29 UTC
RTC time: Tue 2019-02-19 06:16:29
Time zone: America/Port-au-Prince (EST, -0500)
System clock synchronized: no
NTP service: inactive
RTC in TZ: no
```

- 3. Configure the chronyd service on server to synchronize the system with the NTP time source.example.com.

3.1. Edit the /etc/chrony.conf file to specify the classroom.example.com server as the NTP time source. You may use sudo vim /etc/chrony.conf command to edit the configuration file. The following output shows the configuration you must add to the configuration file:

```
...output omitted...
server classroom.example.com iburst
...output omitted...
```

The preceding line in the /etc/chrony.conf configuration file includes the iburst to speed up initial time synchronization.

3.2. Use the timedatectl command to turn on the time synchronization on server.

```
[student@server-a ~]$ sudo timedatectl set-ntp yes
```

The preceding timedatectl activates the NTP server with the changed settings in /etc/chrony.conf configuration file. The preceding timedatectl command may activate either the chronyd or the ntpd service, based on what is currently installed on the system.

- 4. Verify that the settings on server are configured to synchronize with the classroom.example.com time source in the classroom environment.

4.1. Use the timedatectl command to verify the synchronization.

```
[student@server-a ~]$ timedatectl
Local time: Tue 2019-02-19 01:52:17 EST
Universal time: Tue 2019-02-19 06:52:17 UTC
RTC time: Tue 2019-02-19 06:52:17
Time zone: America/Port-au-Prince (EST, -0500)
System clock synchronized: yes
NTP service: active
```

# CHAPTER 2 | Analyzing and Tuning Logs

RTC in local TZ: no

> NOTE
If the preceding output shows that the clock is not synchronized, wait for two seconds and re-run the timedatectl command. it takes a few seconds to successfully synchronize the time settings with the time source.

4.2. Use the chronic command to verify the servera system is currently synchronizing its time settings with the classroom.example.com source.

```
[student@servera ~]$ chronic sources -v
210 Number of sources = 1
  Source mode = servera, '= = peer, '# = local clock.
  / . Source state '*' = current synced, '+ = combined, '-' = not combined,
  / | '?' = unreachable, 'x' = time be in error, '-' = time variable.
  | | | | |
  xxxx [ yyyy ] +/ zzzz
  Reachability register (octal) --
  xxxx = adjusted offset,
  yyyy = measured offset,
  ZZZZ = estimated error.
  Log(2(Polling interval) ---
MS Name/IP address         Stratum Poll Reach Rx Last sample
```

```
^* classroom.example.com 2 377 62 +105us [+143us] +/- 14ms
```

Notice that the preceding output shows an asterisk (*) in the source state ($) field for the classroom.example.com NTP time source. The asterisk indicates that the local system is currently in successful synchronization with the NTP time source.

# 4.3. Log out of servera.

```
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation ~]$
```

# Finish

On workstation, run lab log-maintain finish to complete this exercise. This script ensures that the original time zone is restored along with all the original time settings on servera.

```
[student@workstation ~]$ lab log-maintain finish
```

This concludes the guided exercise.

# ANALYZING AND STORING LOGS

PERFORMANCE CHECKLIST
In this lab, you will change the time zone on an existing server and configure a new log file for all events related to authentication failures.

OUTCOMES
You should be able to:

* Update the time zone on an existing server.
* Configure a new log file to store all messages related to authentication failures.

BEFORE YOU BEGIN
Log in to workstation as student using student as the password.

On workstation, run lab log-review start to start the exercise. This script records the current time zone of the serverb and ensures that the environment is setup correctly.

```
[student@workstation ~]$ lab log-review start
```

- 1. From workstation, open an SSH session to serverb as student.
2. For the sake of this activity, pretend that the serverb system has been relocated to Jamaica and you must update the time zone appropriately. Use sudo to elevate the privileges of the student user while running the timedatectl command to update the time zone. Use student as the password.
3. Display all the log events recorded in the previous 30 minutes from current time on serverb.
4. Create the /etc/rsyslog.d/auth-errors.conf with the necessary lines to help the syslog service write messages related to authentication and security issues to the /var/log/auth-errors file. Use the authpriv facility and the alert priority.

# Evaluation

On workstation, run the lab log-review command to confirm success of this exercise.

```
[student@workstation ~]$ lab log-review grade
```

# Finish

On workstation, run lab log-review finish to complete this lab. This script ensures that the original time zone is restored along with the original time settings on server.

```
[student@workstation ~$ lab log-review finish
```

This concludes the guided exercise.

# CHAPTER 1 | Analyzing and Storing Logs

# SOLUTION

# ANALYZING AND STORING LOGS

### PERFORMANCE CHECKLIST
In this lab, you change the time zone on an existing server and configure a new log file for all events related to authentication failures.

### OUTCOMES
You should be able to:

* Update the time zone on an existing server.
* Configure a new log file to store all messages related to authentication failures.

### BEFORE YOU BEGIN
Log in to workstation as student using the password.

On workstation, run `lab log-review` to start the exercise. This script records the current time zone of the `server` system and ensures that the environment is set correctly.

```
[student@workstation ~$] lab log-review
```

- 1. From workstation, open an SSH session to server as student.
```bash
[student@workstation ~]$ ssh@server
...output omitted...
[student@server ~$]
```

- 2. For the sake of this activity, pretend that the `server` system has been relocated to Jamaica and you must update the time zone. Use `sudo` to elevate the privileges of the student while running the `timedatectl` command to update the time zone. Use student if asked.
- 2.1. Use the `timedatectl` command to view the list of available time zones and determine the appropriate time zone for Jamaica.
```bash
[student@server ~$] timedatectl list-timezones | grep Jamaica
America/Jamaica
```
- 2.2. Use the `timedatectl` command to set the time zone of the `server` system to `America/Jamaica`.
```bash
[student@server ~$] sudo timedatectl set-timezone America/Jamaica
[sudo] password for student: student
```

- 2.3. Use the `timedatectl` command to verify that the time zone is successfully set to America/Jamaica.
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

- 3. Display all the log events in the previous 30 minutes from current time on current server.
3.1. Use the `date` command to determine the time frame for which you want to view the journal entries.
```
[student@server ~]$ date
Feb 22 07:31:05 EST 2019
[student@server ~]$ date -d "-30 minutes"
Feb 22 07:01:35 EST 2019
```

3.2. Use the `--since` and `--until` units with the `journalctl` command to display all log events recorded in the previous 30 minutes on server. To `journalctl`
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

# 4. Create the /etc/rsyslog.d/auth-errors.conf with the necessary lines to help the syslog service write messages related to authentication and security issues to the /var/log/auth-errors file. Use the authpriv facility and the alert priority.

new /var/log/auth-errors file. Use the authpriv facility and the alert priority in the configuration file.

+   4.1. Create the /etc/rsyslog.d/auth-errors.conf file to specify the new /var/log-auth-errors as the destination for messages related to authentication and security issues. You may use the sudo vim /etc/rsyslog.d/auth-errors.conf command to create the configuration file.

authpriv.alert /var/log/auth-errors

+   4.2. Restart the rsyslog service so that the changes in the configuration file take effect.

```
[student@server] $ sudo systemctl restart rsyslog
```

+   4.3. Use the logger command to write a new message to the /var/log/auth-errors file. Apply the -p authpriv.alert option with the logger command to generate a log message relevant to authentication and security issues.

```
[student@server] $ logger -p authpriv.alert "Logging test authpriv.alert"
```

+   4.4. Use the tail command to confirm that the /var/log/auth-errors file is populated with the log entry containing Logging test authpriv.alert message.

```
[student@server] $ sudo tail /var/log/auth-errors
Feb 19 11:56:07 server student [6038]: Logging test authpriv.alert
```

+   4.5. Log out of server.

```
[student@server] $ exit
logout
Connection to server closed.
[student@workstation~]$
```

# Evaluation

On workstation, run the lab log-review grade command to confirm success of this exercise.

```
[student@workstation~]$ lab log-review grade
```

# Finish

On workstation, run lab log-review finish to complete this lab. This script ensures the original time zone is restored along with all the original time settings on server.

```
[student@workstation~]$ lab log-review finish
```

This concludes the guided exercise.
# TABLE 24.2 Message Priority Designations (continued)

| Message Priority | Priority | Description |
| --- | --- | --- |
| =priority | N/A | Log messages of only the specified priority. |
| ! priority | N/A | Ignore messages of the specified priority and higher. |
| != priority | N/A | Log all messages except those of the specified priority. |

# TABLE 24.3 Logging Action Designations

| Action Designation | Description |
| --- | --- |
| absolute path | Log messages to the specified file. |
| /dev/console or /dev/tty | Log messages to the specified terminal. |
| @host | Log messages to the remote host. |
| userid | Send messages to the specified user, if the user is logged in. You can specify multiple user IDs by separating each user ID from the others with a comma. |
| * | Send messages to all logged users via the wall command. |

```
 /syslog.conf
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*
/dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none
/var/log/messages
```
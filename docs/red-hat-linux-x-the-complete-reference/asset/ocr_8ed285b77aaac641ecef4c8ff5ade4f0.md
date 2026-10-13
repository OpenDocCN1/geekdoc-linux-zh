# Table 27-9: Syslogd Facilities, Priorities, and Operators

| Facilities | Description |
|---|---|
| kern | Kernel messages |
| lpr | Line printer subsystem messages |
| mail | Mail subsystem messages |
| mark | Internal use only |
| news | Usenet news subsystem messages |
| syslog | Syslog internal messages |
| user | Generic user-level messages |
| uucp | UUCP subsystem messages |
| local0 through local7 | Reserved for local use |
| Priorities | Description |
|---|---|
| debug | 7. Debugging messages, lowest priority |
| info | 6. Informational messages |
| notice | 5. Notifications, normal, but significant, condition |
| warning | 4. Warnings |
| err | 3. Error messages |
| crit | 2. Critical conditions |
| alert | 1. Alerts, action must be taken immediately |
| emerg | 0. Emergency messages, system is unusable, highest priority |
| Operators | Description |
|---|---|
| * | Matches all facilities or priorities in a sector |
| = | Restrict to a specified priority |
| ! | Exclude specified priority and higher ones |
| / | A file to save messages to |
| @@ | A host to send messages to |
| | | FIFO pipe to send messages to |

# /etc/syslog.conf Example

The default /etc/syslog.conf file for Red Hat systems is shown here. Messages are logged to various files in the /var/log directory.

/etc/syslog.conf

```
# Log all kernel messages to the console.
#kern.*				/dev/console
```
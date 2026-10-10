| Priority | Description |
| :------- | :---------- |
| debug    | Indicates all information from a certain facility |
| info     | Indicates normal information messages as a result of system operations |
| notice   | Indicates information that should be noted for future reference, yet does not indicate a problem |
| warning or warn | Indicates messages that might be the result of an error but are not critical to system operations |
| error or err | Indicates all other error messages not described by other priorities |
| crit     | Indicates system critical errors such as hard disk failure |
| alert    | Indicates an error that should be rectified immediately, such as a corrupt system database |
| emerg or panic | Indicates very serious system conditions that would normally be broadcast to all users |

Table 10-5  Priorities used by the System Log Daemon

```
# Provides TCP syslog reception
$ModLoad imtcp
$InputTCPServerRun 514
```

# Working with the Systemd Journal Daemon

The Systemd Journal Daemon (journald) replaces the System Log Daemon on Linux distributions that use Systemd, such as Fedora 20. As with the System Log Daemon, journald creates a socket (`/dev/log`) for other system processes to write to and reads any information that is written to this socket. However, the events logged are not controlled by specific rules. Instead, journald logs all information to a database under the `/var/log/journal` directory structure, and events are tagged with labels that identify the same facility and priority information that we examined earlier with the syslogd daemon.

![](bbox=[0.146, 0.694, 0.654, 0.77])

To view events within the journald database, you can use the same `journalctl` command that we introduced in Chapter 6 to view boot-related messages. If you type `journalctl` at a command prompt and press the Tab key, you will see a list of areas and criteria that can be queried, as shown here:

```
[root@server1 ~]# journalctl
_AUDIT_LOGINUID=         _MONOTONIC_TIMESTAMP=
_AUDIT_SESSION=          _PID=
_BOOT_ID=                PRIORITY=
```
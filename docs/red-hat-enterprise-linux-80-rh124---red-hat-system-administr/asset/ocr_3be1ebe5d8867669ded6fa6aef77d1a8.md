# PRESERVING THE SYSTEM JOURNAL

# OBJECTIVES

After completing this section, you should be able to configure the system journal to preserve the record of events when a server is rebooted.

# STORING THE SYSTEM JOURNAL PERMANENTLY

By default, the system journals are kept in the /run/log/journal directory, which means the journals are cleared when the system reboots. You can change the configuration settings of system-journal service in the /etc/systemd/journal.conf file to make the journals persist across reboot.

The Storage parameter in the /etc/systemd/journal.conf file defines whether to store journals in a volatile manner or persistently across reboot. Set this parameter to persistent, volatile or auto as follows:

+   * persistent: stores journals in the /var/log/journal directory which persists across reboots.

If the /var/log/journal directory does not exist, the systemd-journal service creates it.

+   * volatile: stores journals in the /var/log/journal directory.
* As the /run file system is temporary and exists only in the runtime memory, data stored in it, including system journals, do not persist across reboot.
* auto: rsyslog determines whether to use persistent or volatile storage. If the /var/log/journal directory uses persistent storage, otherwise it uses volatile storage.

This is the default action if the Storage parameter is not set.

The advantage of a persistent journal is that the historic data is available immediately at boot. However, even with a persistent journal, not all data is kept. The journal has a built-in log rotation mechanism that triggers monthly. In addition, the journals are not allowed to grow larger than 10% of the file system it is on, or less than 15% of the file system free. These values can be tuned for both the runtime and persistent journals in /etc/systemd/journal.conf. The first process starts. The command output shows the entries that reflect the current size limits.

```
[user@host ~]$ journalctl | grep -E 'Runtime|System journal'
Feb 25 13:01:48 remotehost.example.com systemd-journal[548]: Runtime (/var/log/journal/ae60bd8c7da894213da8087fea9229) is 8.0M, max 91.4M, 83.4M free.
(/run/log/journal/7ab164a2e27048be9bf80e06714a8cd5): System journal is 8.0M, max 91.4M, 83.4M free.
```
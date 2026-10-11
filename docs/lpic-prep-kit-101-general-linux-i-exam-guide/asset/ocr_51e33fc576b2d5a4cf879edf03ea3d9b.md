The minus sign (-) before the name of the log will prevent the file from being synced every time it changes. Normally, when a message is written to a log it is written to RAM and then added to the file on the disk immediately. Using the - before the log's name results in the message being saved to RAM but not written to the disk until the next routine synchronization of RAM to disk.

![](bbox=[0.11, 0.25, 0.15, 0.3])

# Key Concept

When specifying the types of messages to log, the `*`, `!`, and `=` characters are extremely helpful. Use the `*` to specify either all message sources or all message types. The `!`, on the other hand, means *not*. Specifying `!*` before a message type would mean none of the following message types.

# Managing Logs

Each message that is written to a log includes the date and source, as well as the message, on a single line. By default, you have the main system log, which is `/var/log/messages`. Depending on the services you have running and how you have configured `syslogd`, you might have many more.

Other system logs that you might have are `/var/log/wtmp`, `/var/log/utmp`, and `/var/log/lastlog`. Each of these contains information on users, which is used by various utilities. Table 10.6 shows how these logs are used.

Table 10.6 Log Files that Record User Logins and the Utilities That Use This Information
| Log File | Contents |
| :--- | :--- |
| `/var/log/wtmp` | Contains login times and duration for each user; used by the `last` command |
| `/var/log/utmp` | Contains information on currently logged-in users; used by the `who`, `w`, and `findex` commands |
| `/var/log/lastlog` | Contains login times for users; used by the `lastlog` command |


The `last` command shows all logins listed in the `/var/log/wtmp` file. Its output can list users more than once. The `who` and `w` commands are used to determine who is presently logged in to the system. The `w` command also shows the time the user logged in. The `finget` command can be used to see the information contained in the comments field of the `/etc/passwd` file for logged-on users.

The minus sign (-) before the name of the log will prevent the file from being synced every time it changes. Normally, when a message is written to a log it is written to RAM and then added to the file on the disk immediately. Using the - before the log's name results in the message being saved to RAM but not written to the disk until the next routine synchronization of RAM to disk.

![](img/8c0f494a2e9a2273fb49af52267f311e_259_0.png)

### Key Concept

When specifying the types of messages to log, the `*`, `!`, and `=` characters are extremely helpful. Use the `*` to specify either all message sources or all message types. The `!`, on the other hand, means *not*. Specifying `!*` before a message type would mean none of the following message types.

## Managing Logs

Each message that is written to a log includes the date and source, as well as the message, on a single line. By default, you have the main system log, which is `/var/log/messages`. Depending on the services you have running and how you have configured `syslogd`, you might have many more.

Other system logs that you might have are `/var/log/wtmp`, `/var/log/utmp`, and `/var/log/lastlog`. Each of these contains information on users, which is used by various utilities. Table 10.6 shows how these logs are used.

Table 10.6 Log Files that Record User Logins and the Utilities That Use This Information

| Log File | Contents |
| :--- | :--- |
| `/var/log/wtmp` | Contains login times and duration for each user; used by the `last` command |
| `/var/log/utmp` | Contains information on currently logged-in users; used by the `who`, `w`, and `finget` commands |
| `/var/log/lastlog` | Contains login times for users; used by the `lastlog` command |

The `last` command shows all logins listed in the `/var/log/wtmp` file. Its output can list users more than once. The `who` and `w` commands are used to determine who is presently logged in to the system. The `w` command also shows the time the user logged in. The `finget` command can be used to see the information contained in the comments field of the `/etc/passwd` file for logged-on users.

The `lastlog` command is used to display the contents of `/var/log/lastlog`. If no options are used, `lastlog` displays the `lastlog` entries ordered by the UID. Using the `-t` option will cause `lastlog` to display all logins during the last specified number of days. You also can use the `-u` option to display the specified user’s last login.

The `lastlog` output also will indicate whether a user has never logged in to the system. Sample output of the `lastlog` command looks like

| Username | Port | From | Latest |
| :--- | :--- | :--- | :--- |
| root | tty1 | | Fri Nov 5 19:21:04 1999 |
| hadn | tty0 | 192.168.0.123 | Fri Nov 12 07:49:45 1999 |
| peanut | tty1 | | Wed May 19 10:33:53 1999 |
| eddie | tty3 | | Sat Aug 21 19:11:05 1999 |
| ronmairt | tty2 | | Sun May 16 16:10:07 1999 |
| mary | | | **Never logged in** |

## Rotating Logs

Because logs can get very large, you will want to monitor them. Periodically you will want to clear the log. When you do this, you will need to decide whether you want to save the old information. This is referred to as rotating the logs.

One way to handle this is to periodically copy or move each log that you want to save to another location. Next, you would either need to recreate the log file (if you moved the original) or empty the original log (if you copied it).

This enables you to save older logs while also improving system performance. As the number of old logs increases, you will need to decide whether you want to archive them or just delete the older logs. This will depend on what the role of your computer is and your organization’s policies. If it is a standalone computer, chances are you will not want to keep older logs.

To simplify this process, you can use the `logrotate` command. The `logrotate` command gives you the ability to automatically rotate your logs, compress or remove old logs, and even mail the log files. This activity can be based on time (such as daily) or on log size.

The syntax for `logrotate` is

```
logrotate [options] config_file
```

By default, `logrotate` saves its status information to `/var/lib/logrotate.status`, but this behavior can be overridden by using the `-s` option and the name of another file.

More than one config file can be passed to the logrotate command; however, instructions contained in the last one named can override instructions in an earlier named file. Table 10.7 lists the commands that can be used in the config files.

Table 10.7 Commands Used in Config Files to Be Used with the **logrotate** Command

| Command | Action |
| :------ | :----- |
| `compress` | Uses gzip to compress old logs |
| `copytruncate` | Copies log then truncates old log |
| `create` | Applies named permissions to new log; if no permissions are specified, permissions of old log are used |
| `daily` | Rotates logs daily |
| `delaycompress` | Compresses on next rotation |
| `errors mailto` | Mails errors to specified address |
| `ifempty` | Rotates empty log |
| `include filename` | Reads `filename` into config file |
| `mail mailto` | Mails logs to specified address when deleting |
| `monthly` | Rotates logs monthly |
| `nocompress` | Does not compress |
| `nocopytruncate` | Does not copy and truncate |
| `nocreate` | Does not use permissions specified by `create` |
| `nodelaycompress` | Compresses now |
| `noolddir` | Does not move to another directory |
| `notifempty` | Does not compress empty log |
| `olddir directory` | Moves old logs to specified directory |
| `postrotate` | Runs script after log is rotated |
| `prerotate` | Runs script before log is rotated |
| `rotate n` | Specifies number of old logs to retain |
| `size n` | Rotates when log reaches `n` bytes; add `k` to specify kilobytes or `M` to specify megabytes |

A configuration file can have both global and local options. *Global* options are applied to all log files, whereas *local* options are applied only to a specific file. Any local options will override global ones. The following is a sample configuration file:

```
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# mail errors to root
error mail root

# create new (empty) log files after rotating old ones
create

# compress old log files
compress

# use configuration files contained in /etc/logrotate.d directory
include /etc/logrotate.d

# will only rotate wtmp monthly instead of weekly
/var/log/wtmp {
    monthly
}
```

In the preceding sample configuration file, the following global options were set:

- frequency of rotation
- number of old logs to keep
- compress old logs

The last section sets local options for the `wtmp` log only by specifying to rotate it monthly instead of weekly. Using local options enables you to configure specific logs with different parameters from the default ones you want to use for the majority of your logs.

### Key Concept

> The `logrotate` command automates the process of saving and removing the contents of your log files. One or more configuration files can be used to define how `logrotate` handles each log.

### Archiving Logs

Now that you have configured `logrotate` to handle logs the way you want, you need to decide how long you will keep old logs. In some instances, you might want to keep some logs for a year or so.

In the earlier configuration file, `logrotate` was configured to keep logs for four weeks. After you have four weeks worth of logs, the oldest log is discarded and `log.3` becomes `log.4`, `log.2` becomes `log.3`, `log.1` becomes `log.2`, and the current log is `log`. You now have four old logs (`log.1`, `log.2`, `log.3`, and `log.4`) as well as the current `log`.

At any one time, you have the current log and the prior four weeks' logs. What if you want to keep information for six months?

When running a Web server, you might want to retain your logs for six months to document attempts to breach your system. Your organization might want to keep records of when users log in and log out for several years. How many logs and how long you keep them will be different based on your organization's policies.

One way to keep logs for a long time would be to increase the number of logs that are kept. However, this could soon fill up your disk, especially if you want to keep logs for several months or years.

A better plan would be to move the older logs to another location. You might even want to move them offline to a tape or other media. Chapter 11, “Backup and Restore,” covers managing backups in more detail.

You can use the *prerotate* command in your configuration file to run a script that will move the oldest log before rotating the logs. In this manner, you can keep logs for as long as you want and have the space to store them.

![](img/8c0f494a2e9a2273fb49af52267f311e_263_0.png)

### Key Concept

The *logrotate* command can be configured to keep as many logs for as long as you want. However, in order to save space, consider moving older logs to another location. The *prerotate* command can be used to move older logs before rotating. This saves space while still saving logs for an extended period of time.

## Using Logs to Troubleshoot

One of the most frequent uses for log files is troubleshooting your system. To diagnose problems when booting your system, you can use the *dmesg* command to display system messages from the kernel ring buffer. The syntax for *dmesg* is

```
dmesg [options]
```

If you want to review a specific level of message, you can use the *-n level* option. If you want to see only panic messages, then use the following command:

```
dmesg -n 1
```

Although other messages will not be displayed, they will still be recorded and *syslogd* will continue to save them to the appropriate logs. Each level of message is defined in the *kernel.h* file. Check the one on your system to identify what the values are for your system.


## Listing 4.2: Sample /etc/logrotate.conf File

```
# Rotate logs weekly
weekly

# Keep 4 weeks of old logs
rotate 4

# Create new log files after rotation
create

# Compress old log files
compress

# Refer to files for individual packages
include /etc/logrotate.d

# Set miscellaneous options
notifempty
nomail
noolddir

# Rotate wtmp, which isn't handled by a specific program
/var/log/wtmp {
    monthly
    create 0664 root utmp
    rotate 1
}
```

Most of these lines set options that are fairly self-explanatory or that are well explained by the comments that typically immediately precede them—for instance, the *weekly* line sets the default log rotation interval to once a week. If you see an option in your file that you don't understand, consult the *logrotate* man page.

The last few lines of Listing 4.2 demonstrate the format for the definition for a specific log file. These definitions begin with the filename for the file (multiple filenames may be listed, separated by spaces), followed by an open curly brace (`{`). They end in a close curly brace (`}`). Intervening lines set options that may override the defaults. For instance, the */var/log/wtmp* definition in Listing 4.2 sets the *monthly* option, which tells the system to rotate this log file once a month, overriding the default *weekly* option. Such definitions are common in the individual files in /etc/logrotate.d, which are typically owned by the packages whose log files they rotate. Examples of features that are often set in these definitions include the following:

-   **Rotated file naming** Ordinarily, rotated log files acquire numbers, such as *messages.1* for the first rotation of the *messages* log file. Using the *dateext* option causes the rotated log file to obtain a date code instead, as in `messages-20100205` for the rotation performed on February 5, 2010.

### Compression options
As already noted, `compress` causes `logrotate` to compress log files to save space. This is done using `gzip` by default, but you can specify another program with the `compresscmd` keyword, as in `compresscmd bzip2` to use `bzip2`. The `compressoptions` option enables you to pass options to the compression command (say, to improve the compression ratio).

### Creating new log files
The `create` option causes `logrotate` to create a new log file for use by the system logger or program. This option takes a file mode, owner, and group as additional options. Some programs don't work well with the `create` option, though. Most of them use the `copytruncate` option instead, which tells `logrotate` to copy the old log file to a new name and then clear all the data out of the original file.

### Time options
The `daily`, `weekly`, and `monthly` options tell the system to rotate the log files at the specified intervals. These options aren't always used, though; some configurations use a size threshold rather than a time threshold for when to rotate log files.

### Size options
The `size` keyword sets a maximum size for a log file. It takes a size in bytes as an argument (adding `k` or `M` to the size changes it to kilobytes or megabytes). For instance, `size 100k` causes `logrotate` to rotate the file when it reaches `100KB` in size.

### Rotation options
The `rotate x` option causes `x` copies of old log files to be maintained. For instance, if you set `rotate 2` for the `/var/log/messages` file, `logrotate` will maintain `/var/log/messages.1` and `/var/log/messages.2`, in addition to the active `/var/log/messages` file. When that file is rotated, `/var/log/messages.2` is deleted, `/var/log/messages.1` is renamed to `/var/log/messages.2`, `/var/log/messages` becomes `/var/log/messages.1`, and a new `/var/log/messages` is created.

### Mail options
If you use `mail address`, `logrotate` will e-mail a log file to the specified address when it's rotated out of existence. Using `nomail` causes the system to not send any e-mail; the log is quietly deleted.

### Scripts
The `prerotate` and `postrotate` keywords both begin a series of lines that are treated as scripts to be run immediately before or after log file rotation, respectively. In both cases, these scripts end with the `endscript` keyword. These commands are frequently used to force `syslogd` or a server to begin using a new log file.

In most cases, servers and other programs that log data either do so via the system logging daemon or ship with a configuration file that goes in `/etc/logrotate.d` to handle the server's log files. These files usually do a reasonable job; however, you might want to double-check them. For instance, you might discover that your system is configured to keep too many or too few old log files for your taste, in which case adjusting the `rotate` option is in order. You should also check the `/var/log` directory and its subdirectories every now and then. If you see huge numbers of files accumulating, or if files are growing to unacceptable sizes, you may want to check the corresponding `logrotate` configuration files. If an appropriate file doesn't exist, create one. Use a working file as a template, modifying it for the new file. Pay particular attention to the `prerotate` or `postrotate` scripts; you may need to consult the documentation for the program that’s creating the log file to learn how to force that program to begin using a new log file.

## Using a Remote Server for Log Files

As noted earlier in “Setting Logging Options,” you can configure `syslogd` to send its logs to a remote computer instead of or in addition to logging data locally. This configuration is fairly straightforward on the system that’s doing the logging: in `/etc/syslog.conf`, you provide a computer hostname preceded by an at-sign (@) rather than a local filename. For instance, this line causes all kernel messages to be logged to `logger.pangaee.edu`:

```
kernel.*		@logger.pangaee.edu
```

You can use other selectors, of course, as described earlier in “Setting Logging Options.” Using this feature enables you to search log files for problems from a central location and provides an additional degree of tamper resistance, since an intruder would need to compromise the logging server as well as the primary target of a computer in order to erase evidence of an intrusion from log files.

Ordinarily, `syslogd` 1.3 and later doesn’t accept logs sent to it from remote systems. Thus, if you have two computers and configure one computer to send some or all of its logs to the other computer, they won’t appear in the logging server’s logs by default. To have the logging system accept such submissions, you must launch `syslogd` with its `-r` option. Precisely how you do this varies from one distribution to another. This daemon is normally launched from a SysV startup script, such as `/etc/init.d/syslog`. You may be able to modify this script to pass the `-r` parameter to `syslogd`. Most `syslogd` SysV startup scripts, though, pass parameters to the daemon using a variable, such as `SYSLOGD_PARAMS`. This variable is most frequently set in another file, such as `/etc/sysconfig/rsyslog` (used by Fedora and Red Hat). Some distributions set the variable in the startup script itself; for instance, Debian and Ubuntu set the `SYSLOGD` variable in the `/etc/init.d/sysklogd` startup script, enabling you to set this option in the startup script. If you need to change these features, do so and then restart the `syslogd` daemon using its own SysV startup script:

```
# /etc/rc.d/init.d/syslog restart
```

The exact name of the SysV startup script varies from one system to another. You must also restart the system logger on the system doing the logging after you make changes to its `/etc/syslog.conf` file. Once this is done, the messages from all the computers configured to log to the logging system should appear in its logs. They should normally be identified by system name:

```
Feb 27 13:17:00 speaker /USR/5B1N/CRON[28223] : (rodsmitH) CMD ->
(/usr/bin/fetchmail -f /home/rodsmith/.fetchmailrc-powmew > /dev/null)
Feb 27 13:18:04 hairloppr111aR ntpd[2036] : kernel time sync enabled 0001
```

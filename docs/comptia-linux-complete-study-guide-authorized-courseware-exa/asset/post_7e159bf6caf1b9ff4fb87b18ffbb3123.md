
use if you're instructed to do so in documentation or if you understand the networking issues involved.

### Log a file
You can log the contents of a file by using the `-f file` option. Be cautious with this option; if `file` is big, your system log file can grow to ridiculous size!

### Identify a priority
The `-p pri` option specifies a priority, as described earlier.

### Log tags
By default, `logger` includes its name in the log file as a tag. You can change this tag with the `-t tag` option. This is useful if you want to identify a script or other program that created the log entry and don't care to record the fact that `logger` was involved in the process.

### Specify a socket
Ordinarily, `logger` calls the default system log tools to do its job. You can log directly to a network socket using the `-u socket` option, if you prefer.

### Specify a message
If you don't specify a file using `-f file`, `logger` will log whatever you type after other options as the message to be logged. If you don't provide a message on the command line, `logger` accepts input you type on subsequent lines as information to be logged. You should terminate such input by pressing Ctrl+D.

As an example, suppose you want to log the message "shutting down for system maintenance" to the system log. You can do so by typing the following command:

```bash
$ logger shutting down for system maintenance
```

The result will be an entry like the following, probably in `/var/log/messages`:

```bash
Jul 29 14:09:50 nessus logger: shutting down for system maintenance
```

Adding parameters changes the details of what's logged, as just described. You can place a call to `logger` in a script as a way of documenting the script's activities. For instance, a system backup script might use `logger` to record details such as its start and stop times and the number and size of the files it has backed up.

## Rotating Log Files

Log files are intended to retain information about system activities for a reasonable period of time; but system logging daemons provide no means to control the size of log files. Left unchecked, log files can therefore grow to consume all the available space on the partition on which they reside. To avoid this problem, Linux systems employ log file rotation tools. These tools rename and optionally compress the current log files, delete old log files, and force the logging system to begin using new log files.

The most common log rotation tool is a package called `logrotate`. This program is typically called on a regular basis via a cron job. (The upcoming section "Running Jobs in the Future" describes cron jobs in more detail.) The `logrotate` program consults a configuration file called `/etc/logrotate.conf`, which includes several default settings and typically refers to files in `/etc/logrotate.d` to handle specific log files. A typical `/etc/logrotate.conf` file includes several comment lines, denoted by hash marks (`#`), as well as lines to set various options, as illustrated by Listing 7.1.

### Listing 7.1: Sample /etc/logrotate.conf File

```bash
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

Most of the lines in Listing 7.1 set options that are fairly self-explanatory or that are well explained by the comments that immediately precede them—for instance, the `weekly` line sets the default log rotation interval to once a week. If you see an option in your file that you don't understand, consult the man page for `logrotate`.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_413_0.png)

Because log file rotation is handled by cron jobs that typically run late at night, it won't happen if a computer is routinely turned off at the end of the day. This practice is common with Windows workstations but is uncommon with servers. Either Linux workstations should be left running overnight as a general practice or some explicit steps should be taken to ensure that log rotation occurs despite routine shutdowns. The `anacron` utility, described in the upcoming section “Using anacron,” is particularly well suited to this task.

The last few lines of Listing 7.1 demonstrate the format for the definition of a specific log file. These definitions begin with the filename for the file (multiple filenames may be listed, separated by spaces), followed by an open curly brace (`{`). They end in a close curly brace (`}`). Intervening lines set options that may override the defaults. For instance, the `/var/log/wtmp` definition in Listing 7.1 sets the `monthly` option, which tells the system to rotate this log file once a month, overriding the default `weekly` option. Such definitions are common in the individual files in `/etc/logrotate.d`, which are typically owned by the packages whose log files they rotate. Examples of features that are often set in these definitions include:

- **Rotated file naming** Ordinarily, rotated log files acquire numbers, such as `messages.1` for the first rotation of the `messages` log file. Using the `dateext` option causes the rotated log file to obtain a date code instead, as in `messages-20091005` for the rotation performed on October 5, 2009.
- **Compression options** As already noted, `compress` causes `logrotate` to compress log files to save space. This is done using `gzip` by default, but you can specify another program with the `compresscmd` keyword, as in `compresscmd bzip2` to use `bzip2`. The `compressoptions` keyword enables you to pass options to the compression command (say, to improve the compression ratio).
- **Creation of new log files** The `create` option causes `logrotate` to create a new log file for use by the system logger or program. This option takes a file mode, an owner, and a group as additional options. Some programs don't work well with this option, though. Most of them use the `copytruncate` option instead, which tells `logrotate` to copy the old log file to a new name and then clear all the data out of the original file.
- **Time options** The `daily`, `weekly`, and `monthly` options tell the system to rotate the log files at the specified intervals. These options aren't always used; some configurations use a size threshold rather than a time threshold for when to rotate log files.
- **Size options** The `size` keyword sets a maximum size for a log file. It takes a size in bytes as an argument (adding `k` or `M` to the size changes it to kilobytes or megabytes, respectively). For instance, `size 100k` causes `logrotate` to rotate the file when it reaches 100KB in size.
- **Rotation options** The `rotate x` option causes `x` copies of old log files to be maintained. For instance, if you set `rotate 2` for the `/var/log/messages` file, `logrotate` will maintain `/var/log/messages.1` and `/var/log/messages.2` in addition to the active `/var/log/messages` file. When that file is rotated, `/var/log/messages.2` is deleted, `/var/log/messages.1` is renamed to `/var/log/messages.2`, `/var/log/messages` becomes `/var/log/messages.1`, and a new `/var/log/messages` is created.
- **Mail options** If you use `mail address`, `logrotate` will e-mail a log file to the specified address when it's rotated out of existence. Using `nomail` causes the system to not send any e-mail; the log is quietly deleted.
- **Scripts** The `prerotate` and `postrotate` keywords both begin a series of lines that are treated as scripts to be run immediately before or after the file log rotation, respectively. In both cases, these scripts end with the `endscript` keyword. These commands are frequently used to force `syslogd` or a server to begin using a new log file.

In most cases, servers and other programs that log data either do so via the system logging daemon or ship with a configuration file that goes in `/etc/logrotate.d` to handle the server’s log files. These files usually do a reasonable job, but you may want to double-check them. For instance, you might discover that your system is configured to keep too many or too few old log files for your taste, in which case adjusting the `rotate` option is in order. You should also check the `/var/log` directory and its subdirectories every now and then. If you see huge numbers of files accumulating, or if files are growing to unacceptable size, you may want to check the corresponding `logrotate` configuration files. If an appropriate file doesn’t exist, create one. Use a working file as a template, modifying it for the new file. Pay particular attention to the `prerotate` and `postrotate` scripts; you may need to consult the documentation for the program that’s creating the log file to learn how to force that program to begin using a new log file.

In most cases, log files remain on the computer that recorded them. Sometimes, though, you may want to copy such files off-site. The easiest way to do this may be to reconfigure the log daemon to send the messages you want to archive to another system, as described in “Setting Logging Options.” Another possibility is to create a cron job (as described later, in “Running Jobs in the Future”) to copy files to another system using a network share, `ssh`, or some other network tool. You can also manually copy log files onto removable disks, if you like. There are few technical reasons to archive log files for more than a few weeks—if a problem escapes your notice for a long time will they be useful. Managers or lawyers may want to keep them around for the long term for business or legal reasons, though.

## Reviewing Log File Contents

Log files do no good if they simply accumulate on the system. Their purpose is to be used as a means of identifying problems or documenting normal activity. When a server isn’t responding as you expect, when a computer refuses login it should be accepting (or accepting logins it should be refusing), or when a system’s network interface isn’t coming up (to name just three types of problems), you should check your log files as part of your troubleshooting procedures. Log files can also be useful in less troublesome situations, such as helping you to identify the load on a server so as to plan upgrades. Several procedures, many of which involve tools described elsewhere in this book, can help you access your log files:

- **Paging through whole log files** You can use a pager program, such as `less` (described in Chapter 1, “Exploring Linux Command-Line Tools”), to view the entire contents of a log file. A text editor can fill the same role.
- **Searching for keywords** You can use `grep` (described in Chapter 1) to pull lines that contain keywords out of log files. This can be particularly handy when you don’t know which log file is likely to hold an entry. For instance, typing `grep eth0 /var/log/*` locates all lines in all files in the `/var/log` directory that contain the string `eth0`.
- **Examining the start or end of a file** You can use the `head` or `tail` command (described in Chapter 1) to examine the first or last several lines of a log file. The `tail` command is particularly handy; you can use it to look at the last few entries just after you take some action that you expect to produce some diagnostic log file entries.

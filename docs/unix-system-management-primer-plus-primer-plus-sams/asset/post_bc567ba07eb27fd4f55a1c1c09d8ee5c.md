
# UNIX SYSTEM MANAGEMENT PRIMER PLUS

# LISTING 12.1 Continued

```
# run commands
shellcommands:
restart_httpd:
    /usr/local/apache/bin/apachectl restart
```

You can add even more flexibility to your configuration by using compound classes. Compound classes support logical AND and OR classes so you can run actions based on the value of multiple classes, not just one. Logical AND is represented by a '&', while logical OR is represented by a '|'. Logical AND is not indicated by preceding a class with a '1'. Using the cfengine.conf in Listing 12.2 to copy the Apache configuration file to the Web servers on Mondays, you could change the configuration to read like this:

```
copy:
    webservers.Monday:
        # Apache configuration to join the web servers
        /usr/repo/files/httpd.conf dest=/usr/local/apache/httpd.conf owner group=root mode=644 define=restart_httpd
```

By now it should be apparent how powerful cfengine can be. You can copy files, uncommon lines, restart processes whatever you want—all from one configuration file.

# Automating Temporary Space Management

Unix provides several default locations for temporary file storage, the most common being /tmp and /var/tmp. You may provide other locations for temporary storage. Users, applications, and the operating system all make use of this space keeping temporary storage locations clean is of critical importance. The tools discussed in the following sections make periodic cleaning a simple part of system maintenance.

# Temporary Space Management Using find

One of the time-honored methods of cleaning out temporary storage directories is by using the find command. find is an unbelievably complex command and many beginning users (even some advanced users) are intimidated by its syntax. The examples offered here use just a few of its options.

Most sites choose to manage temporary storage by removing files that have not been modified in a specified amount of time, such as two weeks. Sometimes the time frame isn't enough—what if some servers have long-running processes that store persistent information in /tmp? Fortunately find can be as specific as you need it to. One method that works is instructing find to delete only files that are owned by users, not by administrative accounts. For example, if most servers are run as root, you can tell find to ignore those files. The following find command removes files over two weeks that do not belong to root:

```
# find /tmp /var/tmp -mtime +14 ! -user root rm -f {} \
```

# Monitor File Removal

You may want to add the -print option to the end of this find and redirect the output to a file or email so you can monitor the removal of files.

# Temporary Space Management Using cfengine

The tidy action of cfengine can be used to "tidy" temporary directories in a format that's much easier to understand than its syntax. Specify the directory to tidy up and any of the following attributes to match files you want removed:

| pattern=wildcard | Matches the filename with this pattern, using optional shellcards |
| :--- | :--- |
| recurse=number|inf | Sets the number of directories to recurse, or inf for infinite recursion. |
| age=days | Sets the minimum age of a file in days. |
| type=atimectime | Specifies which time attribute to match a file's age. The default is modified time, or mtime. |
| size=number|empty | Specifies the size of a file. Append k or kb for kilobytes, mb or mb for megabytes, and so on. Match empty files with size=empty |
| rdirs=true|false|all|sub | Specifies whether to remove directories. By default, cfengine does not delete directories. Setting this to true deletes only empty directories, all will delete all directories that match the criteria or not they are empty, and sub deletes only subdirectories of the searched directory. |

Delete files and empty directories that have not been modified in over two weeks from the /tmp directory, use the following configuration:

- - tidy:
  /tmp pattern=* recurse=inf age=14 type=mtime rdirs=true

What makes cfengine great for performing tasks like this is that you can separate different directory cleaning requirements into classes. For instance, on an interactive login server you may want to clean out /tmp every week, but on a DNS server you may never want to clean it out.

# Automating Log Maintenance

All Unix systems have an abundance of log files. There are log files for the kernel, for mail, for Web servers, and most other Unix applications in existence today. The problem with log files is that they can grow to enormous sizes if not trimmed or rotated regularly; searching through a 2GB log file for a single piece of data can take a bit of time, especially if you are not sure of the log file you are looking for. They can also fill your file system or drive, which is even more catastrophic.

Many utilities exist for rotating logs; some are provided with the operating system, and some are available from third parties. Almost all modern Unix vendors, Solaris and Red Hat Linux included, at the very least provide a mechanism for rotating local system logs generated by syslog. Using the messages as an example, rotation works by renaming messages to messages.1, and restarting syslog so it recreates the original log files. Even older logs are kept in messages.2, messages.3, and on a typical log directory on Red Hat Linux is full of these:

```
ls /var
XFree86.0log cron.4 messages.1 secure statistics
boot.log dmesg messages.2 secure.1 wtmp
boot.1 htmlaccess.log messages.3 secure.2 wtmp.1
boot.2 lastlog messages.4 secure.3 xdm-errors
boot.3 maillog netconf.log secure.4 spooler xferlog
boot.4 maillog netconf.1 spooler xferlog.1
cron.1 maillog netconf.2 spooler.1 xferlog.2
cron.2 maillog netconf.3 spooler.2 xferlog.3
cron.3 messages sa netconf.4 spooler.3 xferlog.4
```

When rotating a log file, the operating system must first rename older logs to make room for the new log. For example, if you were keeping four logs at a time, messages.4 would be deleted, messages.3 would be renamed to messages.4, messages.2 would be renamed to messages.3, and messages.1 would be renamed to messages.2. The operating system handles this renaming automatically; Solaris uses /usr/lib/newslog and Red Hat Linux uses logrotate; newslog is a simple script written for Solaris log rotation. logrotate is a generic program that can handle the rotation of any log; learn more about it in the next section.

# Log Rotation and Open Files

Open file handling requires one major caveat when rotating logs. Many applications—including syslog—will keep files open after being opened. Renaming an open log does not rotate the file—logging process is still holding that file and will write to it. Without this feature you may have to stop and restart the program to rotate logs, and that is not an option in production environments.

# Using logrotate as a Generic Rotation Tool

Red Hat Linux runs logrotate as a daily cron job to maintain its own log files, but few people take advantage of logrotate to manage their own application logs.
Information pertaining to each log and its rotation policies are stored in a configuration file:
/etc/logrotate.conf by default. To maintain state between runs, logrotate stores the time of last rotation of each log in a "state file," /var/lib/logrotate.status on RedLinux. The state file ensures that logrotate does not rotate logs more than once per day, unless an administrator accidentally runs it more than once.

logrotate has a very simple syntax, as follows:
logrotate [-dv] [-f|--force] [-s|--state-file] config-file

The logrotate -d option enables debugging mode and performs a dry run of the configuration.\Verbose mode is enabled with -v and will produce output explaining each task it

The logrotate command has a few options—the real magic lies in the configuration file.
Default configuration is stored in /etc/logrotate.conf and looks like this:

```
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# send errors to root
errors root

# create new (empty) log files after rotating old ones
create

# uncomment this if you want your log files compressed
#compress

# RPM packages drop log rotation information into this directory
include /etc/logrotate.d

# no packages own lastlog or wtmp .. we'll rotate them here
/var/log/wtmp {
monthly
create 0664 root wtmp
rotate 1
}
```

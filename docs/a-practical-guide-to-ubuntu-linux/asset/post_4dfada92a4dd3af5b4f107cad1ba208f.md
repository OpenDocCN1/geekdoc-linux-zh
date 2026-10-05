
# # create new (empty) log files after rotating old ones
create

# uncomment this if you want your log files compressed
#compress

# packages drop log rotation information into this directory
include /etc/logrotate.d

```
# no packages own wtmp, or btmp -- we'll rotate them here
/var/log/wtmp {
missingok
monthly
create 0664 root utmp
rotate 1
}
```

```
/var/log/btmp {
missingok
monthly
create 0664 root utmp
rotate 1
}
```

# system-specific logs may also be configured here.

The logrotate.conf file sets default values for common parameters. Whenever logrotate reads another value for one of these, it resets the default value. You have a choice of rotating files daily, weekly, or monthly. The number following the rotate keyword specifies the number of rotated log files you want to keep. The create keyword allows logrotate to create a new log file with the same name and attributes as the newly rotated log file. The compress keyword causes log files to be compressed using gzip. The include keyword specifies the /etc/logrotate.d directory for program-specific specification files. When you install a program using dpkg (page 532) or a dpkg-based utility such as aptitude (page 526), the installation script puts the logrotate specification in this directory.

The last sets of instances in logrotate.conf take care of the /var/log/wtmp and /var/log/btmp log file holds login records; you can view this file with the command who /var/log/wtmp. The keyword missingok overrides the implicit default value of nonmissingok for this utility only (because the value is within brackets). This keyword allows logrotate to continue without introducing an error message if the log file is missing. The keyword monthly overrides the default value of weekly. The create keyword is followed by the arguments establishing the permissions, owner, and group for the new file. Finally rotate establishes that rotated log files be kept.

The /etc/logrotate.d/cups file is an example of a utility-specific logrotate specification file:

```
$ cat /etc/logrotate.d/cups
/var/log/cups/*log {
  daily
  missingok
  rotate 7
  sharedscripts
  prerotate
  if [ -e /var/run/cups/cupsd.pid ]; then
    invoke-rc.cd --quiet cups force-reload > /dev/null
    sleep 10
  fi
  endscript
  compress
  notempty
  create 640 root lpadmin
}
```

This file, which is installed by the cups package install script and incorporated in /etc/logrotate.d because of the include statement in logrotate.conf, works with each of the files in /var/log/cups that has a filename ending in (*log). The sharedscripts keyword causes rotate to execute the command(s) in the prerotate and postrotate sections only one time—not one for each log that is rotated. Although it does not appear in this example, the copytruncate keyword causes logrotate to rotate the original log file immediately after it copies it. This keyword is useful for programs that cannot be restarted to reopen their log files because they might continue writing to the original file even after it has moved. The logrotate utility executes the commands between prerotate and script before the rotation begins. Similarly, commands between postrotate and endscript are executed after the rotation is complete. The notempty keyword logrotate not to rotate the log if it is empty, overriding the default action of rotating empty log files.

The logrotate utility works with a variety of keywords, many of which take arguments and have side effects. Refer to the logrotate page for details.

# REMOVING UNUSED SPACE FROM DIRECTORIES

A directory that contains many filenames is inefficient. The point at which a directory on an ext2, ext3, or ext4 filesystem becomes inefficient varies, depending partly on the length of the filenames. Best practice is to keep directories relatively small. Having a few hundred files (or directories) in a directory is generally a good idea, and having more than thousand versus thousand is generally a bad idea. Additionally, Linux uses a caching mechanism for frequently accessed files that speeds the process of locating an inode from a filename. This caching mechanism works only on filenames of up to 30 characters in length, to avoid giving frequently accessed files extremely long filenames.

When a directory becomes too large, you can usually break it into several smaller directories by moving its contents to these new directories. Make sure you remove the original directory once you have moved all of its contents.

# SOLVING PROBLEMS

Because Linux directories do not shrink automatically, removing a file from a directory does not shrink the directory, even though it frees up space on the disk. To remove unused space and make a directory smaller, you must copy or move all the files to a new directory and make the original directory.

The following procedure removes unused space. First remove all unneeded files from the large directory. Create a new, empty directory. Next move or copy all remaining files from the old directory to the new empty directory. Remember to copy hidden files. Finally delete the directory and rename the new directory.

```
$ sudo mkdir /home/max/new
$ sudo mv /home/max/large/* [A-Z]* /home/max/new
$ sudo rmdir /home/max/large
$ sudo mv /home/max/new /home/max/large
```

# optional

# DISK QUOTA SYSTEM

The quota system (supplied by the quota software) limits the disk space and number of files owned by individual users. You can choose to limit each user's disk space, the number of files each user can own, or both. Each resource has two limits: a lower limit and an upper limit. The user can exceed the lower limit, or quota, although a warning is given each time the user logs in he is above the quota. After a number of warnings (set by the system administrator), the system behaves as if the user had reached the upper limit. Once the upper limit is reached or the user has received the specified number of warnings, the user will not be allowed to create any more files or use any disk space. The user's only recourse at that point is to remove some files.

Users can review their usage and limits with the quota utility. Using sudo, you can use quota to obtain information about any user. You can quota only if the filesystem is mounted with the usquota and/or grquota options (ext3 and ext4 filesystems).

First you must decide which filesystems to limit and how to allocate space among users. Typically only filesystems that contain users' home directories, such as /home, are limited. Use the equota utility to set the quotas, and use quota start the quota system. Unmounting a filesystem automatically disables the quota for that filesystem.

# rsyslogd: LOGS SYSTEM MESSAGES

Traditionally UNIX programs send log messages to standard error. If a permanent log was required, the output was redirected to a file. Because of the limitations of this approach, 4.3BSD introduced the log daemon (rsyslogd) now used by Linux. This daemon listens for log messages and stores them in the /var/log hierarchy. In addition to providing logging facilities, rsyslog allows a single machine to serve as a log repository for a network and allows arbitrary programs to process log messages.

The /etc/rsyslog.conf file stores configuration information for rsyslog while the /etc/rsyslog.d/50-default.conf file stores default rules for rsyslog. Each line in the 50-default.conf contains one or more selectors and an action, separated by whitespace. The selectors define the origin and type of the message; the action specifies how rsyslog processes the message. Sample lines from rsyslog.conf (a # indicates a comment):

```
# First some standard logfiles. Log by facility.
kern.* -/var/log/kern.log
lpr.* -/var/log/lpr.log
mail.* -/var/log/mail.log

# Some "catch-all" logfiles.
*.debug=\auth,authpriv.:\nnews.name:mail.name:\n*.info:;*:warning:\ -/var/log/debug
auth,authpriv.:\ncron,daemon.*: -/var/log/messages
*
# Emergencies are sent to everybody logged in.
*.emerg
```

The priority indicates the severity of the message. The following list of the priority names and the conditions they represent appears in priority order:

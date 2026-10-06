
## RPM packages drop log rotation information into this directory
include /etc/logrotate.d

# no packages own wtmp -- we'll rotate them here
/var/log/wtmp {
  monthly
  create 0664 root root
  rotate 1
}

system-specific logs may also be configured here.
Whenever logrotate runs into another value for one of these parameters, it resets the default value. You have a choice of rotating files daily, weekly, or monthly. The number keyword specifies the number of rotated log files that you want to keep. The create keyword causes logrotate to create a new log file with the same name and attributes as the newly rotated log file. The compress keyword (commented out in the default file) causes log files to be compressed using gzip. The include keyword specifies the standard /etc/logrotate.d directory for program-specific log specification files.
When install a program using rpm (page 928), rpm puts the corresponding log specification file (if it is part of the package) in this directory.

The last set of instructions in logrotate.conf takes care of the /var/log/wtmp file (/var/log/wtmp). The rotate monthly overrides the default value of weekly for this utility only (because the value is within brackets). The create keyword is followed by the arguments establishing the permissions, owner, and group for the new file. Finally, rotate establishes that one rotated log file should be kept.
/etc/logrotate.d/samba is a utility-specific logrotate specification file:

```bash
$ cat /etc/logrotate.d/samba
/var/log/samba/*.log {
  notifempty
  missingok
  sharedscripts
  copytruncate
  postrotate
  /bin/kill -HUP `/var/run/samba/smbd.pid /var/run/samba/nmbd.pid` 2>/dev/null 2|||| true
  endscript
}
```

This file, is incorporated in /etc/logrotate.d because of the include statement, works with each of the files in /var/log/samba that has a filename extension of log (*log). The notifempty keyword causes logrotate not to rotate the log file if it is empty, overriding the default action of rotating log files. The missingok keyword means that no error will be issued when the file is missing. The sharedscripts keyword causes logrotate to execute the command(s) in the prerotate and postrotate sections one time, not one for each log that is rotated. The copytruncate keyword causes logrotate to truncate the original log file immediately after it copies it. This keyword is useful for programs that cannot be instructed to close and reopen their log files, as they may continue writing to the original file even after it has been moved. The commands between postrotate and endscript are executed after the rotation is complete. Similarly, commands between prerotate and endscript are executed before the rotation is started.

The logrotate utility has many keywords and many of these take arguments and have side effects. Refer to the logrotate page for details.

## Removing Unused Space from Directory

A directory with too many files in it is inefficient. The point at which a directory on an ext2 or ext3 filesystem becomes inefficient varies, depending on the length of the filenames it contains. Keep your directories relatively small. Having fewer than a few hundred files (or directories) in a directory is generally a good idea, and having more than a few thousand is a bad idea. Additionally, GNU/Linux uses a caching mechanism for frequently accessed files to speed the process of locating an inode from a file. This mechanism works only on filenames up to 30 characters in length, so avoid extremely long filenames for frequently accessed files.

When you find a directory that is too large, you can usually break it into several smaller directories by moving its contents into new directories. Make sure that you remove the original directory once you have moved its contents.

Because GNU/Linux directories do not shrink automatically, removing a file from a directory does not shrink the directory, even though it makes more space on the disk. To remove unused space and make a directory smaller, you must copy or move all the files into a new directory and remove the original directory.

The following procedure removes unused directory space. First, remove all needed files from the large directory. Then create a new, empty directory. Next, move or copy all the remaining files from the old large directory to the new directory. Remember to copy hidden files. Finally, delete the old directory and rename the new:

```bash
# mkdir /home/alex/new
# mv /home/alex//* /home/alex/large/. [A-z]* /home/alex/new
# rmdir /home/alex/large
# mv /home/alex/new /home/alex/large
```

## Optional

## Disk Quota System

The disk quota system limits the disk space and number of files owned by individual users. You can choose to limit each user's disk space, the number of files each user can own, or both.

## Getting Help

Each resource that is limited has two limits. The lower limit, or quota, can be exceeded by the user, while a warning is presented each time the user logs in when he or she is above the quota. After a certain number of warnings (set by the system administrator), the system will behave as if the user had reached its upper limit. Once the upper limit is reached or the user has received the specified number of warnings, the user will not be allowed to create any more files or any more disk space. The user's only recourse at that point is to remove some.

Users can review their usage and limits with the quota.

## Chapter Summary

This chapter defines a system administrator as someone who keeps the system useful and convenient for users and describes some of that person's tasks. Many of these files are located in /etc. Much of the work you do requires you to log in as root. The chapter describes the special privileges of the root user (called Superuser). When you are logged in as Superuser, you have extensive powers that you do not have.

When you bring up the system, it is sometimes single-user mode. In this mode only the system console is functional, and not all the filesystems are mounted. When the system is in single-user mode, you can back up files and use fsck to check the integrity of filesystems before you mount them. The utility brings the system to its normal multiuser state. With the system in multiuser mode, you can still perform many administration tasks, such as adding users and printers.

The installation section of this chapter explains the process of installing GNU/Linux. But because of all the possible options, many of the details are left to the documentation and the Linux Kernel HOWTO.

As a system administrator you need to keep all the software on the system up-to-date; You will need to add and remove rpm software packages, as well as GNU configure and build system packages. Toward this end Red Hat and other vendors have programs that automate software update retrieval and installation. Red Hat's product is Red Hat Network.

The chapter describes system operation: booting up, running rc scripts, single-user mode, emergency mode, multiuser mode, bringing the system down, and what to do when the system crashes.
G/Linux filesystem, introduced in Chapter 4, is described in detail, listing of important files and directories, types of files, and how to maintain and work with various types of filesystems. With the growth of the GNOME and KDE desktops are GUI administration tools. These tools, including the GNOME System Settings and System windows, as well as KDE's Control Center's System and Network Modules, are covered in detail. Tables that parallel the systems help you work your way through the mazes of menus to present all the tools and options in a GUI format.

The next sections of the chapter describe classic system administration tasks, including setting users and groups, backing up files, and managing printers. The networking system, which delivers into NFS, NIS, DNS, PPP, Samba, DHCP, OpenSSH, and GNU Privacy Guard, is followed by a description of how to rebuild the Linux kernel.

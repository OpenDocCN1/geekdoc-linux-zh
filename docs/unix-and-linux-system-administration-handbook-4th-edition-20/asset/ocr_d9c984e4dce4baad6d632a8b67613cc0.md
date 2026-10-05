# Chapter 11 Syslog and Log Files

Table 11.1 compiles information about some of the more common log files on our example systems. Specifically, it lists the following:

+   - The log files to archive, summarize, or truncate
- The program that creates each
- An indication of how each filename is specified
- The frequency of cleanup that we consider reasonable
- The systems (among our examples) that use the log file
- A description of the file's contents

Filenames in Table 11.1 are relative to /var/adm, /var/log, or /var/log/syslog unless otherwise noted.

Log files are generally owned by root, although conventions for the ownership and mode of log files vary. In some cases, a privileged daemon such as http or mysql may require write access and set the ownership and mode appropriate. You may need sudo to view log files that have tight permissions. Alternatively, for log files that do not contain system details, its is safe to change the permissions to be world-readable. We recommend the latter method for log files you need to view regularly, such as Apache’s logs in /var/log/httpd.

Syslog maintains many of the log files in Table 11.1, its default configuration varies widely among systems. With a consistent etc/syslog.conf the log files would have more in common among operating systems.

Log files can grow very quickly, especially the logs for busy services such as email, web, and DNS servers. An out-of-control log file can fill up the disk and bring the system to its knees. For this reason, we need to keep a separate partition for the noisiest and busiest log files. On Linux systems, /var or /var/log is a good choice. Other systems’ conventions vary, but plan ahead when building a new box.

# Files not to manage

Most logs are text files which are written as interesting events occur. But a few of the logs listed in Table 11.1 have a different context.

wtmp (sometimes wtmp) contains a record of users’ logins and logouts as well as entries that record when the system was rebooted or shut down. It is a fairly generic file in that new entries are simply added to the end of the file. However, the wtmp file is maintained in a binary format. Use the last command to decode the information.

lastlog contains similar information to that in wtmp, but it records only the time of last login for each user. It is a sparse, binary file that is indexed by UID. It may stay smaller if your UIDs are assigned in some kind of numeric sequence, although this is nothing to sleep over in the real world. lastlog doesn’t need to be rotated because its size stays constant unless users log in.

See the footnote on page 308 for more info about sparse files.
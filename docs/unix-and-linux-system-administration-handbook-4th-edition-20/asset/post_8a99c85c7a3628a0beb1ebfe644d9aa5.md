
# Chapter 11 Syslog and Log Files

Table 11.1 compiles information about some of the more common log files on our example systems. Specifically, it lists the following:

- The log files to archive, summarize, or truncate
- The program that creates each
- An indication of how each filename is specified
- The frequency of cleanup that we consider reasonable
- The systems (among our examples) that use the log file
- A description of the file's contents

Filenames in Table 11.1 are relative to /var/adm, /var/log, or /var/log/syslog unless otherwise noted.

Log files are generally owned by root, although conventions for the ownership and mode of log files vary. In some cases, a privileged daemon such as http or mysql may require write access and set the ownership and mode appropriate. You may need sudo to view log files that have tight permissions. Alternatively, for log files that do not contain system details, it is safe to change the permissions to be world-readable. We recommend the latter method for log files you need to view regularly, such as Apache’s logs in /var/log/httpd.

Syslog maintains many of the log files in Table 11.1, its default configuration varies widely among systems. With a consistent etc/syslog.conf the log files would have more in common among operating systems.

Log files can grow very quickly, especially the logs for busy services such as email, web, and DNS servers. An out-of-control log file can fill up the disk and bring the system to its knees. For this reason, we need to keep a separate partition for the noisiest and busiest log files. On Linux systems, /var or /var/log is a good choice. Other systems’ conventions vary, but plan ahead when building a new box.

# Files not to manage

Most logs are text files which are written as interesting events occur. But a few of the logs listed in Table 11.1 have a different context.

wtmp (sometimes wtmp) contains a record of users’ logins and logouts as well as entries that record when the system was rebooted or shut down. It is a fairly generic file in that new entries are simply added to the end of the file. However, the wtmp file is maintained in a binary format. Use the last command to decode the information.

lastlog contains similar information to that in wtmp, but it records only the time of last login for each user. It is a sparse, binary file that is indexed by UID. It may stay smaller if your UIDs are assigned in some kind of numeric sequence, although this is nothing to sleep over in the real world. lastlog doesn’t need to be rotated because its size stays constant unless users log in.

See the footnote on page 308 for more info about sparse files.

# Table 11.1 Log files on parade

| File | Program | Where* | Freq* | Systems* | Contents |
|---|---|---|---|---|---|
| acpid | acpid | F | 64k | RZ | Power-related events |
| auth.log | sudo, etcᵇ | S | M | U | Authorizations |
| apache2/* | httpd (v2) | F | D | ZU | Apache HTTP server logs (v2) |
| apt* | API | F | M | U | Aptitude package installations |
| boot.log | rc scripts | Fᶜ | M | R | Output from system startup scripts |
| boot.msg | kernel | H | - | Z | Dump of kernel message buffer |
| cron, cron/log | cron | S | W | HAR | cron executions and errors |
| cups/* | CUPS | F | W | ZR | Printing-related messages (CUPS) |
| daemon.log | various | S | W | U | All daemon facility messages |
| debug | various | S | D | U | Debugging output |
| dmsg | kernel | F | - | RU | Dump of kernel message buffer |
| dpkg.log | package | F | M | U | Package management log |
| faillogᵈ | login | H | W | RZ | Unsuccessful login attempts |
| httpd/* | httpd | F | D | R | Apache HTTP server logs (in /etc) |
| kern.log | kernel | S | W | U | All kernel facility messages |
| mail* | lastlog | H | - | RZ | Last login time per user (binary) |
| messages | mail-related | S | W | ZRUS | All mail facility messages |
| rmpkgs | cron.daily | H | D | R | List of identified RPM packages |
| samba/* | smbd, etc. | F | W | - | Samba (Windows/CIFS file-sharing) |
| secure | sshd, etc. | S | M | R | Private authorization messages |
| sulog | su | F | SA | SA | successes and failures |
| syslog* | various | S | W | SUH | The main system log file |
| warn | various | S | W | Z | All warning/error-level messages |
| wpars/* | wpar | F | - | A | Workload partition events |
| wtmp | login | H | M | all | Login records (binary) |
| xen/ | Xen | F | 1m | RZ | Xen virtual information |
| xorg.log | Xorg | F | W | RS | Windows server errors |
| yum.log | yum | F | M | R | Package management log |

a. Where: S = Syslog, H = Hardwired, F = Configuration line
Freq: D = Daily, W = Weekly, M = Monthly, [Km] = Size-based, in KB or MB
Systems: U = Ubuntu, Z = Ubuntu, S = SU, Red Hat and CentOS, S = Solaris, H = HP-UX, A = AIX
b. password, login, and shutdown also write to the authorization log. It's in /var/adm.
c. Actually logs through syslog, but the facility and level are configured in /etc/initconfig.conf.
d. Binary file must be read with the lastad utility.

utmp attempts to keep a record of each user that is currently logged in. It is sometimes wrong, usually because a shell was killed with an inappropriate signal and the parent of the shell did not clean up properly. utmp is world-writable.

# Chapter 11 Syslog and Log Files

# Vendor specifics

Vendors seem to have hidden log files over the disk. Careful detective work with your daemons' config files and your syslog configuration file will find many of them. This section details some of the more obscure nooks and crannies in which log files have been hidden.

Linux distributions win the grand prize for simplified log management. Logs are clearly named and consistently stored in /var/log. All our extreme distributions also include a superior tool, lograte, for rotating, truncating, and managing. New software packages can drop a config file into the /etc/lograte.d directory to set up a management strategy for logs. (lograte is covered in detail later in this chapter; see page 356.)

By contrast, Solaris has the most disorganized collection of log files. With a directory called /var/log it shouldn't be so hard. A few pointers:

- /var/log/*
- /var/cron/log
- /var/lp/logs/*
- /var/saf/_log
- /var/saf/zmon/log
- /var/svc/log
- /var/adm/*

You can run the vendor-supplied /usr/lib/newslog script out of cron to rotate the main log files, /var/adm/messages and /var/log/syslog.

HP-UX log files are in /var/adm. A lot of odd little mystery files live in this directory, many of which are not logs, so be careful what you touch. nettl.LOG000 is a network control and statistics file; see metnl for details. By default, entries submitted through syslog go into the /var/adm/syslog directory.

# 11.2 SYSLOG: THE SYSTEM EVENT LOGGER

Syslog, originally written by Eric Allman, is a comprehensive logging system. It has two important functions: to liberate programmers from the tedious mechanics of writing log files, and to put administrators in control of logging. Before syslog, every program was free to make up its own logging policy. System administrators had no control over what information was kept or where it was stored.

Syslog is flexible. It lets you sort messages by their source and route them to a variety of destinations: logs, users' terminals, or other machines. Syslog's ability to centralize logging for a network is one of its most valuable features.

Syslog was long adopted by every major variant of UNIX and Linux with the exception of AIX. Every AIX includes the syslog daemon and library routines, but it supplies no default syslog configuration and uses its own proprietary daemon

# Configuring syslogd

for error reporting. See page 353 later in this chapter for details. Since syslog is so commonly used add-on software, we believe that a thorough understanding of syslog is important even for AIX administrators.

# Syslog architecture

Syslog consists of three parts:

- syslogd, the logging daemon (and its config file, /etc/syslog.conf)
- openlog et al., library routines that submit messages to syslog
- logger, a user-level command that submits log entries from the shell

Syslog is started at boot time and runs continuously; it cannot be managed with inet. Syslog reads messages from /dev/log socket, its configuration file, and dispatches messages to the appropriate destination.

A hangup (HUP, 1) causes syslog to close its log files, reread configuration file, and start logging again. If you modify /etc/syslog.conf, you must send a hangup signal to syslog to make your changes take effect. A TERM signal makes syslog exit.

Syslog writes its process ID to a file in /var/run (etc on AIX). This convention makes it easy to send signals to syslog from a script. For example, the following command sends a hangup:

```
solaris$ kill -HUP /bin/cat /var/run/syslog.pid
```

Trying to rotate a log file that syslog has open for writing is not healthy and has unpredictable results. Refer to page 356 for sane log rotation with the logrotate utility.

The preferred method of restarting syslog on AIX is to use refresh:

```
aix$ sudo refresh -s syslog
```

refresh contacts the System Resource Controller, which manages subsystems as logging. See the refresh man page for more information.

# Configuring syslog

The /etc/syslog.conf file controls syslog'd behavior. It is a text file with a relatively simple format. Blank lines and lines with a pound sign (#) in column one are ignored. The basic format is

```
selector <Tab> action
```

For example, the line

```
mail.info /var/log/maillog own```

causes messages from the email system to be saved in /var/log/maillog. The selector and action fields must be separated by one or more tabs; spaces do not work.

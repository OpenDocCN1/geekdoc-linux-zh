
Before you shut down the server, you should unmount the `/crypt` filesystem as you would any other partition, and you should also disconnect the `ppd0` driver, as follows:

```bash
[ramon]$ sudo umount /crypt
[ramon]$ sudo ppddsetup -d /dev/ppdd0
```

PPDD encrypts an entire filesystem with a key derived from a single passphrase and allows users to access the files within the filesystem using the standard Linux permissions model. This makes PPDD a good candidate for protecting a server’s disk from being read by an intruder who has physically seized the system, as well as for protecting backup media that have fallen into the wrong hands.

## In Sum

This chapter examines the issues involved in system-level Linux security and provides a set of recommended configurations and utilities that can aid in protecting your server from unauthorized access by local users. While all the popular Linux distributions are becoming increasingly security conscious, there are still a staggering number of vulnerabilities being reported daily.

It’s important to understand the impact of all kernel parameters and recognize which ones can have a direct influence on the security of your server. You should build your own custom kernel for efficiency, but also for security and accountability.

You should protect your server against root exploits. One way to do this is by constantly monitoring the permissions of your system files, and by guarding against the perils of `setuid`/`setgid` executables. Setting the correct default `umask` for your users ensures that they’re creating files with a safe set of permissions. Also, limiting the size of core files with the `ulimit` command can prevent a common type of root compromise attack.

When all else fails, filesystem encryption can protect the data that has been compromised. The Cryptographic File System (CFS) provides good granularity for individual protection of user information, while the Practical Privacy Disk Driver (PPDD) is an efficient, transparent method for encrypting filesystems (and backups) in bulk.

The next chapter, Chapter 3, covers the monitoring and auditing of your system and describes the tools that you can use to ensure the integrity of your system files. This is an essential part of system security, and should be used in conjunction with the recommendations in this chapter.

# 3

## System Monitoring and Auditing

Monitoring your system for abnormal behavior is an essential task in both system administration and information security. Most attackers leave their “fingerprints” in the system log files, and examining these logs is a fundamental step in the process of network forensics. More important, examining log files on a regular basis, looking for erratic or suspicious user behavior, can prevent attacks and enhance the overall security of your server.

There are attackers who may be able to penetrate your system without leaving any evidence in the log files. However, even the best attackers will not be able to delete or modify a history file without being noticed. Examining log files is just one critical part of your overall security plan.

You should be looking at the system log files for

- Repeated authentication failures
- Unusual shutdowns
- Attempts to relay messages through your mail server
- Any events that seem out of the ordinary

A single authentication failure for a single user can be attributed to a mistyped password. Multiple authentication failures for a single user can be attributed to an acute case of “fat-finger” syndrome. Multiple authentication failures for multiple users, however, are a clear sign of an attack in the making, or a sign that one of your internal users may be trying to guess the root password in an effort to gain greater access to your server.

Through the use of the centralized syslog facility, Linux offers a wealth of real-time diagnostics that are often not used to their full extent, not because they don’t offer the right kind of information, but because most system administrators don’t know exactly how to use these diagnostics. The problem is that the standard Linux syslog files are too verbose to be of any value. A typical `/var/log/messages` file on a standard Red Hat or Caldera distribution can grow by 500–600K bytes in a typical day for an average-load server.

Human inspection of log files has two major shortcomings:

- The task is tedious and expensive because it has to be performed by a (highly paid) system administrator who is trained to recognize the trouble signs.
- Humans are prone to error, especially when scanning large text files full of repetitive sequences.

Luckily, the Linux community has responded to the challenge and has developed a number of useful log-monitoring tools that can be run batch style to identify certain keywords or patterns that are known to spell trouble. The section “System Log Monitoring” later in this chapter illustrates the concept of log monitoring using two such tools: swatch and logcheck.

## System Logging with syslog

The syslog utility allows the system administrator to configure and manage log files generated by heterogeneous system utilities and applications from a central location. Linux comes standard with the syslog utility configured and the syslgd daemon active upon startup. The system administrator specifies in the `/etc/syslog.conf` file which messages they would like to see logged, and the application directs the messages to the appropriate log file. Most generic messages are directed to the `/var/log/messages` file, although the system administrator can choose any arbitrary file as the destination. In general, Linux uses the following initial log files:

`/var/log/messages` This is the primary Linux log file, used for recording most common system events.

`/var/log/secure` Authentication failures for daemons started from `/etc/inetd.conf` are logged here. (Chapter 4, “Network Services Configuration,” discusses the inetd utility.)

`/var/log/maillog` The sendmail daemon is notoriously verbose (and often very busy), so it makes sense to dedicate this separate log file to keep track of mail-delivery messages.

`/var/log/spooler` This is the log file where other daemons such as UUCP and News (NNTP) log their messages.

`/var/log/boot.log` The boot-up messages displayed when the system is coming up are typically logged in this file.

These five log files are automatically rotated by the system via the /etc/logrotate.d/syslog script. Rotating essentially means renaming the current log file to something like logfile.1 while creating a new (empty) file called logfile to record only those events that took place since the last rotation. At the next rotation, the logfile.1 file is renamed to logfile.2 and the logfile.11 file (if you’re only keeping 10 log files) is deleted.

### syslog.conf File

Listing 3.1 shows a typical syslog.conf file on a Linux system. It includes references to the five log files described earlier in this section.

**Listing 3.1 A typical Linux /etc/syslog.conf file**

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kernel.*                              /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none        /var/log/messages

# The authpriv file has restricted access.
authpriv.*                            /var/log/secure

# Log all the mail messages in one place.
mail.*                                /var/log/maillog

# Everybody gets emergency messages, plus log them on another
# machine.
*.emerg                                 *
*.emerg                                 @loghost

# Save mail and news errors of level err and higher in a
# special file.
uucp,news.crit                        /var/log/spooler

# Save boot messages also to boot.log
local7.*                              /var/log/boot.log
```

The general format of the entries in the syslog.conf file is as follows:

*facility.priority[*;**facility.priority[*] [TAB]*action*

Each field is defined as follows:

*facility*  The *facility* field is the subsystem that you want to log events from. The current supported subsystems are

- auth: secure and authentication messages
- authpriv: private secure and authentication messages
- cron: clock/scheduler daemon
- daemon: other system daemons
- kern: Linux kernel messages
- lpr: line printer system messages
- mail: mail system
- news: network news subsystem
- sysloger: internal syslog messages
- uucp: Unix-to-Unix copy subsystem
- local0–local7: reserved for local use

The special character * can be used to denote any (and all) facilities.

*priority*  The *priority* field specifies the priority level of the message within a given subsystem. The current priorities are (in ascending order of criticality)

- debug: debug-level messages for troubleshooting
- info: informational messages
- notice: normal messages of special interest
- warning: abnormal messages signaling impending failure
- error: failure condition messages
- crit: critical error-condition messages
- alert: condition needing immediate action
- emerg: error condition leading to system failure

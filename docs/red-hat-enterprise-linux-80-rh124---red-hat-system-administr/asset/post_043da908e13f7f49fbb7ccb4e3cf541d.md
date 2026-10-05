
# DESCRIBING SYSTEM LOG ARCHITECTURE

## OBJECTIVES

After completing this section, you should be able to describe the basic logging architecture by Red Hat Enterprise Linux to record events.

## SYSTEM LOGGING

Processes and the operating system kernel record a log of events that happen. These logs are used to audit the system and troubleshoot problems.

Many system records log events in text files that are kept in the `/var/log` directory. These logs can be inspected using normal text utilities such as `less` and `tail`.

A standard logging system based on the Syslog protocol is built into Red Hat Enterprise Linux. Many programs use this service to record and organize them. The `systemd-journal` and `rsyslog` services handle the syslog messages in Red Hat Enterprise Linux 8.

The `systemd-journal` service is at the heart of the operating system event architecture. It collects events from many sources including the kernel, output from the early stages of the boot process, standard and standard error from daemons as they start up and run, and then restructures them into a standard format, and writes them into a structured, indexed system journal. By default, this journal is stored on a file system that does not persist across reboots.

However, the `rsyslog` service reads syslog messages received by `systemd-journal` from the journal as they arrive. It then processes the syslog messages, recording them to log files or forwarding them to other services according to its own configuration.

The `rsyslog` service sorts and writes syslog messages to the log files that do persist across reboots in `/var/log`. The `rsyslog` service sorts the log messages to specific files based on the type of message that each sends, `facility`, and the priority of each syslog message.

In addition to syslog message files, the `/var/log` directory contains log files from other services on the system. The following table lists some useful files in the `/var/log` directory.

## Selected Log Files

| LOG FILE | TYPE OF MESSAGES STORED |
| --- | --- |
| /var/log/messages | Most syslog messages are logged here. Exceptions include messages related to authentication processing, scheduled job execution, and those which are purely debugging-related. |
| /var/log/secure | Syslog messages related to security and authentication events. |
| /var/log/maillog | Syslog messages related to the mail server. |
| /var/log/cron | Syslog messages related to scheduled job execution. |
| /var/log/boot.log | Non-syslog console messages related to system startup. |

> NOTE
Some applications do not use syslog to manage their log messages, although typically, they place their log files in a subdirectory of /var/log. For example, the Apache Web Server saves log messages to files in a subdirectory of the /var/log directory.

## REFERENCES
systemd-journald.service(8), rsyslog(8), and rsyslog.conf(5) man pages

For more information refer to the Using log files to troubleshoot problems section in the Red Hat Enterprise Linux 8.0 BETA Configuring basic system settings Guide at https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8-beta/html/configuring_basic_system_settings/getting-started-with-system-administration#Troubleshoot-log-files

## QUIZ

# DESCRIBING SYSTEM LOG ARCHITECTURE

Choose the correct answer to the following questions:

- 1. Which of these log files stores most syslog messages, with the exception of those that are related to authentication, mail, scheduled jobs, and debugging?
  a. /var/log/maillog
  b. /var/log/boot.log
  c. /var/log/messages
  d. /var/log/secure

- 2. Which log file stores syslog messages related to security and authentication operations in the system?
  a. /var/log/maillog
  b. /var/log/boot.log
  c. /var/log/messages
  d. /var/log/secure

- 3. Which service sorts and organizes syslog messages into files in /var/log/
  a. rsyslog
  b. systemd-journal
  c. auditd
  d. tuned

- 4. Which directory accommodates the human-readable syslog files?
  a. /sys/kernel/debug
  b. /var/log/journal
  c. /run/log/journal
  d. /var/log

- 5. Which file stores syslog messages related to the mail server?
  a. /var/log/lastlog
  b. /var/log/maillog
  c. /var/log/tallylog
  d. /var/log/boot.log

- 6. Which file stores syslog messages related to the scheduled jobs?
  a. /var/log/cron
  b. /var/log/tallylog
  c. /var/log/spooler
  d. /var/log/secure

- 7. What file stores console messages related to system startup?
  a. /var/log/messages
  b. /var/log/cron
  c. /var/log/boot.log
  d. /var/log/secure

## SOLUTION

# DESCRIBING SYSTEM LOG ARCHITECTURE

Choose the correct answer to the following:

- 1. Which of these log files stores most syslog messages, with the exception of those that are related to authentication, mail, scheduled jobs, and debugging?
  a. /var/log/maillog
  b. /var/log/boot.log
  c. /var/log/messages
  d. /var/log/secure

- 2. Which log file stores syslog messages related to security and authentication operations in the system?
  a. /var/log/maillog
  b. /var/log/boot.log
  c. /var/log/messages
  d. /var/log/secure

- 3. Which service sorts and organizes syslog messages into files in /var/log/
  a. rsyslog
  b. systemd-journald
  c. auditd
  d. tuned

- 4. Which directory accommodates the human-readable syslog files?
  a. /sys/kernel/debug
  b. /var/log/journal
  c. /run/log/journal
  d. /var/log

- 5. Which file stores syslog messages related to the mail server?
  a. /var/log/lastlog
  b. /var/log/maillog
  c. /var/log/tallylog
  d. /var/log/boot.log

- 6. Which file stores syslog messages related to the scheduled jobs?
  a. /var/log/cron
  b. /var/log/tallylog
  c. /var/log/spooler
  d. /var/log/secure

- 7. What file stores console messages related to system startup?
  a. /var/log/messages
  b. /var/log/cron
  c. /var/log/boot.log
  d. /var/log/secure

## REVIEWING SYSLOG FILES

After completing this section, you should be able to interpret events in relevant syslog files to troubleshoot problems or recover system status.

## LOGGING EVENTS TO THE SYSTEM

Many programs use the syslog protocol to log events to the system. Each log message is categorized by a facility (the type of message) and a priority (the severity of the message). Available facilities are documented in the syslog.conf(5).

The following table lists the eight syslog priorities from highest to lowest.

| CODE | PRIORITY | SEVERITY |
| --- | --- | --- |
| 0 | emerg | System is unusable |
| 1 | alert | Action must be taken immediately |
| 2 | crit | Critical condition |
| 3 | err | Non-critical condition |
| 4 | warning | Warning condition |
| 5 | notice | Normal but significant event |
| 6 | info | Informational event |
| 7 | debug | Debugging-level message |

The syslog service uses the facility and priority of log messages to determine how to handle them. This is configured by rules in the /etc/syslog.conf file and in the /etc/syslog.d directory that has a file extension of .conf. Software packages can easily add rules by installing an appropriate file in the /etc/syslog.d directory.

Each rule controls how to sort messages is a line in one of the configuration files. The left side of each line indicates the facility and severity of the syslog message rule matches. The right side of each line indicates what to save the log message (or where to deliver the message). An asterisk (*) is a wildcard that matches all values.

For example, the following line would record messages sent to the authpriv facility at any priority to the file /var/log/secure:

```
authpriv.*                /var/log/secure
```

## CHAPTER 2 Analyzing and Sorting Logs

Log messages sometimes match more than one rule in syslog.conf. In such cases, one message is stored in more than one log file. To limit messages stored, the key word none in the priority field identifies that no messages for the indicated facility should be stored in the given file.

Instead of logging syslog messages to a file, they can be printed to the terminals of all logged-users. The rsyslog.conf file has a setting to print all the syslog messages with the emerg priority to the terminals of all logged-in users.

## SAMPLE RULES OF RSYLOG

#### RULES ####

- # Log all kernel messages to the console.
# Logging much elseut up the screen.
#kern.*

- # Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail;authpriv.none;cron.none

- # The authpriv file has restricted access.
authpriv.*

- # Log all the mail messages in one place.
mail.*

- # Log cron stuff
cron.*

- # Everybody gets emergency messages
*.emerg

- # Save new errors of level crit and higher in a special file.
uucp,news.crit

- # Save boot messages also to boot.log
local7.*

## LOG FILE ROTATION

The logrotate tool rotates logs to keep them from taking too much space in the file system containing /var/log directory. When a log is rotated, it is renamed with an extension indicating the date it was rotated. For example, the old /var/log/messages file may

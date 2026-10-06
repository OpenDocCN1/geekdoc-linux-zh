
# Chapter 7 ♦ Logging 183

| Table 7-3 | logrotate Directives |
| Directive | Description |
| :--- | :--- |
| Compress | Compress the file when it is rotated. |
| dateext2 (SUSE only) | Add a date extension to the rotated log file. For example, access_log.20040527.gz. |
| maxage 365 | If previously rotated log files reach this age, remove them. Age is expressed as an integer of days. |
| rotate num | If a file is rotated num times, then remove the oldest rotated file. |
| Size | If a file to be rotated above the size specified, then rotate it. Size can be specified in various units, such as kilobytes (K) and gigabytes (G). |
| notempty | Do not rotate the file if it is empty. |
| missingok | If a file to be rotated does not exist, issue an error and continue. |
| create 644 root | The file permissions to create the new file. |
| Postrotate /etc/init.d/apache2 | When a rotation has taken place, execute the following. In this case we are telling Apache to reload its configuration. This forces |
| reload endscript | Apache to reopen its log file, completing the rotation process. |

## Analyzing Your Logs with logcheck

When your applications are logging to specific files, and the logs are being rotated daily, you can then manage and view your system statistics daily. If you would like to automate analysis of your log files for major occurrences, logcheck is here for you.

logcheck scans your log files for set security and error messages and emails your findings at prelined times through cron. The logcheck process uses a benchmark feature to send you only the last logcheck run so that you do not receive the same errors for the same log time and again.

logcheck is not included in the SUSE distribution, the authors have created an RPM at www.palmcoder.net/files/suse-rpms/wiley. See Chapter 12 for more information on installing RPM packages. You can also find the logcheck RPM on the book's companion web site at www.wiley.com/suselinux10.

When installed, the logcheck creates an entry in /etc/cron.hourly. Any executable scripts in /etc/cron.hourly will be run every hour. This is appropriate for most busy systems as one logcheck run per root user would produce a very large email to send to the user.

When logcheck runs, it will email the root user to tell him or her of any problems it has across. It is up to the administrator to act upon the email and either fix or investigate the logcheck reports.

The /etc/logcheck directory contains four files. Two of these are used to search through log files in the logcheck.sh file and identify specific types of messages to report, while the other two are used as messages to ignore the log files specified in the logcheck.sh file. If a line in an log file is found, its appearance will not be reported. If on the other a line contains an entry in the logcheck.hacking or logcheck.violations file, its appearance is reported to the administrator.

logcheck does not use a configuration file, but is controlled by the logcheck.sh script, located in /usr/bin/logcheck.sh. By default, the script scan /var/log/messages, /var/log/warn, and /var/log/mail. To add or remove entries in the logcheck.sh file, open the script and find the $LOGTAIL entries in the middle of the file. Listing 7-9 shows an example.

### Listing 7-9: entry for logcheck Log File to Monitor

These entries direct logcheck to append messages from various system log files to a temporary file for later analysis. It is important to realize that the first $LOGTAIL entry copies the log file since the last read and the last two concatenate /var/log/warn and /var/log/mail into the temporary file. The $LOGTAIL environment variable is used to call the log application, which will read in a text file and output only new data since it was last passed through logtail. This stops you from receiving old warnings about log activity.

When the temporary file has been created, the whole file is compared against the hacking and violation files we talked before.

It is a relatively involved process to get logcheck customized, and we have done the hard work for you to get it working with the SUSE RPM we built in Chapter 12. We recommend you use RPM as opposed to the source distribution available unless you know what you are doing.

Listing 7-10 displays an example of mail sent to the root user by logcheck script. Note that under the heading Security Violations are two entries referring to failed login attempts via SSH.

### Listing 7-10: logcheck Example Mail

```
From root@bible.suse.com Thu May 27 23:23:41 2004
X-Original-To: root@bible.suse.com
Delivered-To:
Date: Thu, 27 May 2004 23:23:39 +0100
To: root@bible.suse.com
Subject: bible 05/27/04:23.23 system check
User-Agent: mail 10.6/15/03
MIME-Version: 1.0
Content-Type: text/plain; charset=us-ascii
Content-Transfer-Encoding: 7bit
From: root@bible.suse.com (root)
```

#### Security Violations

```
--------------------------------------
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
```

#### Unusual System Events

```
--------------------------------------
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:35 sshd[5019]: error: PAM: Authentication failure
May 27 23:23:10 bible postfix/postfixlog[3881]: E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
May 27 23:23:10 bible postfix/postfixlog[4941]: message-id=C0B666AB.mail13V42YZ@bible.suse.com E47F918D21: uid=from=<root>
```

When the temporary file has been created, the whole file is compared against the hacking and violation files we talked before.

## Using Webbalizer

Another popular analyzer is webalizer. Figure 7-1 shows webalizer. Webbalizer was specifically written to analyze web traffic. It outputs an HTML page with statistics for the month, day, per hour; ranking of the most popular pages; so on. Figure 7-1 shows webalizer. This enables you to and it will be presented with a screen like Figure 7-2. This enables you to access the web server via Apache. Apache configuration is covered in Chapter 16. This enables you to access the.

## Reading Log Files

This chapter has covered what logging on a SUSE Linux system means and what you can do with the messages that are generated both the kernel and processes that you run.

However, reading logs is a skill in itself. There is no good way to teach people how to read logs; rather, it is something that comes with experience. We will give you your short rundown of common entries you will find in /var/log/messages and explain how to interpret them to help you on your way. The following line is an example of a log entry indicating an SSH login failure:

```
May 27 23:23:35 bible sshd[5019]: error: PAM: Authentication failure
```

From this example, you can see things about log entries that are generic to all of them. The first entry is the date and time this entry was created, with the host

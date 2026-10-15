
## Logfile rotation definitions and options
/var/log/messages {
  postrotate
    /bin/kill -HUP `cat /var/run/syslogd.pid`
  endscript
}
/var/log/samba/*.log {
  notifempty
  copytruncate
  sharedscripts
  postrotate
    /bin/kill -HUP `cat /var/lock/samba/*.pid`
  endscript
}

This configuration rotates /var/log/messages every week. It keeps five versions of the file and notifies syslogd each time the file is reset. Samba log files (of which there may be several) are also rotated weekly, but instead of being moved aside and restarted, they are copied and then truncated. The Samba daemons are sent HUP signals only after all log files have been rotated.

## Table 11.7 logrotate options

| Option | Meaning |
|---|---|
| compress | Compresses all noncurrent versions of the log file |
| daily, weekly, monthly | Rotates log files on the specified schedule |
| delaycompress | Compresses all versions but current and next-most-recent |
| endscript | Marks the end of a prerotate or postrotate script |
| errors emailaddr | Emails error notifications to the specified emailaddr |
| missingok | Doesn't complain if the log file does not exist |
| notifempty | Doesn't rotate the log file if it is empty |
| olddir dir | Specifies that older versions of the log file be placed in dir |
| postrotate | Introduces a script to run after the log has been rotated |
| prerotate | Introduces a script to run before any changes are made |
| rotate n | Includes n versions of the log in the rotation scheme |
| sharedscripts | Runs scripts only once for the entire log group |
| size logsize | Rotates if log file size > logsize (e.g., 100K, 4M) |

logrotate is normally run out of cron once a day. Its standard configuration file is /etc/logrotate.conf, but multiple configuration files (or directories containing configuration files) can appear on logrotate's command line. This feature is used to great effect by Linux distributions, which define the /etc/logrotate.d directory as a standard place for logrotate config files. logrotate-aware software packages (of which there are many) can drop in log management instructions as part of their installation procedure, greatly simplifying administration.

In addition to logrotate, Ubuntu provides a simpler program called savelog that manages rotation for individual files. It's more straightforward than logrotate and doesn't use (or need) a config file. Some packages prefer to use their own savelog configurations rather than logrotate.

## 11.5 CONDENSING LOG FILES TO USEFUL INFORMATION

Syslog is great for sorting and routing log messages, but when all is said and done, its end product is still a bunch of log files. While they may contain all kinds of useful information, those files aren't going to come and find you when something goes wrong. Another layer of software is needed to analyze the logs and make sure that important messages don't get lost amid the chatter.

A variety of free tools are available to fill this niche, and most of them are remarkably similar: they scan recent log entries, match them against a database of regular expressions, and process the important messages in some attention-getting way. Tools differ primarily in their degree of flexibility and in the size of their off-the-shelf database of patterns.

Two of the more commonly used log postprocessors are Todd Atkins' swatch and Craig Rowland's logcheck. Both are available from sourceforge.net (logcheck comes with the sentrytools package: sourceforge.net/projects/sentrytools).

swatch is a Perl script that gets its marching orders from a configuration file. The configuration syntax is fairly flexible, and it provides access to the full pattern-matching mojo of Perl. While swatch can process an entire file in a single bound, it's primarily intended to be left running so that it can review new messages as they arrive, a la tail -f. A disadvantage of swatch is that you must build your own configuration essentially from scratch; it doesn't know about specific systems and the actual log messages they might generate.

logcheck is a more basic script written in sh. The distribution also includes a C program that logcheck uses to help it record its place within a log file. logcheck knows how far it has read in a log file, so there is perhaps less chance of a message slipping by at startup or shutdown time. In addition, logcheck can run at intervals from cron rather than running continuously.

logcheck comes with sample databases for several different versions of UNIX and Linux. Even if you don't want to use the actual script, it's worth looking over the patterns to see if there are any you might want to steal for your own use.

These tools have the disadvantage of working on only a single log file at a time. If your syslog configuration sorts messages into many different files, you might want to duplicate some of the messages into a central file that is frequently truncated or rotated, then use that summary file to feed a postprocessing script. That's easier than setting up a complicated network of scripts to handle multiple files.

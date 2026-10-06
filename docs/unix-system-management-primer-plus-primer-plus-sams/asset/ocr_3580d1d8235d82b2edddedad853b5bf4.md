# Chapter 6 • MONITORING SERVICES

archiving with cron (see Chapter 12), or have your backup software manage it for you.
Chapter 9, "Preparing for Disaster Recovery," offers more information on backup software.

As a simple example, the following crontab entry writes all of the message logs to the Solaris
tape device /dev/rmt/00 at 11:00 p.m. on Sunday nights (check your system documentation
for the name of your system's device:

```
0 11 * * * ( cd /var/adm; tar cf /dev/rmt/0 messages* )
```

# Log Monitoring

Most people are content to passively monitor system logs once a day just to make sure everything looks kosher. If something goes wrong, these admin-
trators fix it after the fact. This approach won't do for critical system errors such as a file
system filling up or an operating system panic; you need to know about these things as soon
they have happened.

Fortunately, there are many third-party log-monitoring packages available on the Internet. The
sections discuss one of those packages, logsurfer, which boasts many of the features
y should be looking for in log-monitoring software. You also learn how these packages
notify administrators of errors that occur both during and after normal working hours.

# Log-Monitoring Software

The first well-known log-monitoring software was swatch. Swatch worked well for a basic
monitoring program, but it had its limitations: it required Perl (a more significant problem in
the early 1990s), it could work only with single-line log messages, and it had limited support
dfor dynamic rules.

Enter logsurfer in 1996. Logsurfer overcame all of the limitations of swatch and added a few
features of its, as follows:

+   - Context-sensitive analysis enables you to monitor collections of related logs as one unit.
- Dynamic rules let you create new monitoring rules based on the content of previous
messages.
- Multiple actions can be taken on one log message.
- Individual log messages must pass through two regular expressions to evoke an action—
each that message must match, and (optionally) one that the message must not
match.
- The entire logsurfer program is written in C, with no third-party software requirements.

Logsurfer's configuration file is a set of rules. Rules determine the actions that are taken for
logs that match the patterns you specify. For example, if the program /usr/local/bin/logmail were written to email its standard input to system administrators, the following rule
would send all failures to the administrators:
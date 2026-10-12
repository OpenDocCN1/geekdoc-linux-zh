keywords. The following variables are set to indicate the location of the four LogSentry filter files:

```
HACKING_FILE=/etc/logcheck/logcheck.hacking
VIOLATIONS_FILE=/etc/logcheck/logcheck.violations
VIOLATIONS_IGNORE_FILE=/etc/logcheck/logcheck.violations.ignore
IGNORE_FILE=/etc/logcheck/logcheck.ignore
```

For more information on filter files, see the “Changing LogSentry filter files” section, later in this chapter.

+   * Log files — The last entries in /usr/sbin/logcheck.sh script that you may want to change designate which log files are monitored by the logcheck.sh script. By default, the script runs the logtail command to check the messages, secure, and maillog files (in /var/log). The following lines define which log files are checked and determine where the output of logtail is temporarily written.

```
$LOGTAIL /var/log/messages > $TMPDIR/check.$$
$LOGTAIL /var/log/secure >> $TMPDIR/check.$$
$LOGTAIL /var/log/maillog >> $TMPDIR/check.$$
```

> TIP: If you like, you can have more log files checked by adding more lines like the preceding ones. Just make sure that the first line includes a single arrow (to overwrite a previous check file) and that all subsequent lines contain double arrows (to append to the current check file).

# ## Changing LogSentry filter files

The /etc/logcheck directory contains four filter files that define which messages are matched and e-mailed to the administrator. The contents of these files are simply keywords. Log files are searched (or grepped) for these keywords and sorted or discarded based on the results of the search.

Some keyword filter files are intended to uncover words or phrases that would appear in a log message in the event of a system break-in or misuse. Other keyword files are intended to find messages that pose no security threat (so that the messages can be excluded from the e-mailed log messages). Messages that match neither the included or excluded keywords are appended to the Unusual System Events heading of the e-mail summary output.

You can use filter files as they are. However, over time, you may want to modify these files for several reasons. If you are receiving repetitive, non-threatening messages in the LogSentry e-mails, you can add keywords that can filter out those messages. Also, you can add keywords later as you learn about new types of security breaches that you may want to look for.

Besides including alphanumeric characters, keywords can also include wildcard characters. For example, you could use an asterisk (*) to match any string of characters, a question mark (?) to match any single character, or a dollar sign ($) to match a keyword that appears at the end of a line.
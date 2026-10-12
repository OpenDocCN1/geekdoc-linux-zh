Using the LogLevel directive, you can specify what type of messages Apache should send to syslog. For example, the following instructs Apache to send debug messages to syslog:

```
ErrorLog syslog
LogLevel debug
```

If you want to store debug messages in a different file via syslog, modify `/etc/syslog.conf`. For example,

```
*.
.debug   /var/log/debug
```

Add this line in `/etc/syslog.conf`, restart syslog (`killall -HUP syslogd`), and Apache will enable you to store all Apache debug messages to the `/var/log/debug` file. Also, note that you can set LogLevel to any of the following settings:

+   - **emerg.** Emergency messages
+   - **alert.** Alert messages
+   - **crit.** Critical messages
+   - **error.** Error messages
+   - **warn.** Warnings
+   - **notice.** Notification messages
+   - **info.** Information messages
+   - **debug.** Messages logged at debug level will also include the source file and line number where the message is generated, to help debugging and code development

![](bbox=[0.08, 0.63, 0.15, 0.71])

> If you want to see updates to your syslog or any other log files as they happen, use the tail utility with the `-f /path/to/log` option.

# Analyzing server log files

Many third-party Web server log analysis tools are available. Most of these tools expect the log files to be in CLF format, so make sure you have CLF
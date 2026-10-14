+   - For any priority specified in a selector, all messages of that priority and all higher priorities (more serious problems) are included.
+   - The same messages can be logged to more than one place by including the same selector on multiple lines with different actions. For example, critical kernel messages might be displayed on the /dev/console device and also logged to a remote machine for later analysis using a configuration line such as this:
+     `*.crit    /dev/console,@logging_host`
+   - Configuration lines in syslog.conf do not override previous configuration lines; each action configured by a line in syslog.conf adds to everything already configured.

In addition to these basic rules of syntax for syslog.conf, several special symbols are occasionally used to specify facilities or priorities with greater precision. The man page for syslog.conf has complete details on these rarely used features.

Table 13-5 describes the effect of several sample syslog.conf configuration lines.

# Table 13-5 Sample syslog.conf Configuration Lines

| Sample configuration line | Effect of the configuration line |
|---|---|
| #kern.* /dev/console | None; this line begins with a comment character |
| kern.* /dev/console | Log all kernel messages (of any priority) to the console (the computer screen) |
| *.info,mail.none,authpriv.none /var/log/messages | Log all messages from any facility with a priority of info or higher to the file /var/log/messages, but exclude all messages with a facility of mail or authpriv, no matter what priority |
| authpriv.* /var/log/secure | Log all messages from the authpriv facility to the file /var/log/secure |
| uucp,news.crit /var/log/spooler | Write any messages of priority crit or higher for the facilities uucp or news to the file /var/log/spooler |
| *.emerg * | Display any messages with a priority of emerg on the screen of all users who are logged in |
| mail.* /var/log/maillog | Log all messages from the mail facility to the file /var/log/maillog |
| *.emerg @loghost | Send all messages of priority emerg (from all facilities) to the syslogd daemon running on the computer named loghost |

After changing the syslog.conf configuration file, you must tell syslogd and klogd to reread the configuration file, so that your changes to the file are implemented on your system. You can do this using the service command (the syslog service restarts both logging daemons):

```
# service syslog restart
```
```
/etc/mail/mailer table.db: could not create: Permission
denied
```

In general, do the following to make sure sendmail is safe to run in your
system:

+   Ensure that the /etc/sendmail.cf and /etc/mail/* file and
+   directories are readable by only the superuser or the username you
+   specified in the RunAsUser line in the /etc/sendmail.cf file. All
+   of these files and directories should be writable by the superuser only.
+   Do not enable group write permission for any of the configuration
+   files, directories, or any other files that sendmail needs to read.

Under no circumstances should you enable group write access for any
of the configuration files. Although sendmail allows you to disable the secu-
rity features related to file permissions and ownership by using the Dont
BlameSendmail option, you instead should fix the permission/ownership
problem if any is reported by sendmail in log file. Never disable the checks
in sendmail. If you want to keep the security checks as is, ensure that user
home directories in which .forward files are kept are not writable by any
group. The .forward file itself should have a 644 (rw-r--r--) permis-
sions setting. Also, make sure that any directory that is in the path of file
sendmail reads has group write access disabled.

After you make sure that file/directory level permissions are set proper-
ly, and sendmail doesn't spit out any warning or error message because of
permission/ownership of files and directories, make sure that logging is
properly enabled. By default, sendmail writes logs via syslog, so include
the following line in your /etc/syslog.conf file:

```
mail.*				/var/log/maillog
```

You can change the log filename to your liking; typically, this file is
named mail.log or mail1.log. Also make sure you that you have an entry
such as the following in the /etc/logrotate.d/syslog file:

```
/var/log/maillog {
postrotate
		/usr/bin/killall -HUP syslogd
endscript
}
```
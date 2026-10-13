# Securing your configuration files

Beginning with version 8.9.x, sendmail has tightened the restrictions on configuration file permissions. For example, if I run chmod -R 664 /etc/mail/* to change the file permissions for the configuration files, and then try to restart sendmail, I get the following error messages:

```
Starting sendmail: /etc/sendmail.cf: line 93: fileclass:
cannot open /etc/mail/sendmail.cw: Group writable directory

WARNING: Group writable directory /etc/mail
/etc/mail/virtusertable.db: could not create:
Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/access.db: could not create: Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/domaintable.db: could not create:
Permission denied

WARNING: Group writable directory /etc/mail
/etc/mail/mailertable.db: could not create:
Permission denied
```

In general, do the following to make sure sendmail is safe to run in your system:

+   - Ensure that the /etc/sendmail.cf and /etc/mail/* files and directories are readable by only the superuser or the username you specified in the RunAsUser line in the /etc/sendmail.cf file. All of these files and directories should be writable by the superuser only.
+   - Do not enable group write permission for any of the configuration files, directories, or any other files that sendmail needs to read.

Under no circumstances should you enable group write access for any of the configuration files. Although sendmail allows you to disable the security features related to file permissions and ownership by using the DontBlame Sendmail option, you instead should fix the permission/ownership problem
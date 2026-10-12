+   3. If you want to use a different queue (that is, other than /var/spool/mqueue) for the test configuration, use the -OQ option. For example, /usr/sbin/sendmail -Csendmail-test.cf -OQ/var/spool/test-mqueue uses the /var/spool/test-mqueue directory for the test configuration.

At this point, you should have sendmail configured as expected.

# Securing sendmail

Being one of the oldest mail servers, sendmail has had its share of security holes and blame. The current version of sendmail has been released with strict security in mind.

# Securing your configuration files

Beginning with version 8.11.x, sendmail has tightened the restrictions on configuration file permissions. For example, if I run chmod -R 664 /etc/mail/* to change the file permissions for the configuration files and then try to restart sendmail, I get the following error messages:

```
Starting sendmail: /etc/sendmail.c: line 93: fileclass:
cannot open /etc/mail/sendmail.cw: Group writable directory
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/virtualuserstable.db: could not create: Permission
denied
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/access.db: could not create: Permission denied
```

```
WARNING: Group writable directory /etc/mail
/etc/mail/domaintable.db: could not create: Permission
denied
```

```
WARNING: Group writable directory /etc/mail
```
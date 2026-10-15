+   - **@bypass_spam_checks_maps**. This array includes a list of spam lookup tables. You can disable spam checking by setting this array to "1" (uncomment the line).

Next to @bypass_virus_checks_maps and @bypass_spam_checks_maps, there are two more arrays of the same kind available:
@bypass_banned_checks_maps enables checking for banned names or file types.
@bypass_header_checks_maps enables checking for invalid headers.

+   - **$max_servers**. Number of pre-forked children.
+   Should match the number of your MTA pipe, e.g., the **maxproc** field in /etc/postfix/master.cf.

```
#
=========================================================================
# service type  private unpriv  chroot  wakeup  maxproc command + args
#              (yes)    (yes)   (yes)   (never) (100)
#
=========================================================================
=
smtp     inet  n       -       n       -       2       smtpd -o
content_filter=smtp:[127.0.0.1]:10024
```

+   - **$daemon_user** and **$daemon_group**. User and group to which the daemon will change.

+   - **$mydomain**. The domain name.

+   - **$MYHOME**. Location where the AMaViSd-new files are stored.

+   - **$TEMPBASE**. The path of a temporary directory that can be used by AMaViSd-new. This directory must exist or needs to be created manually.

In the following line an environment variable $TMPDIR is defined with the content of the $TEMPBASE variable.
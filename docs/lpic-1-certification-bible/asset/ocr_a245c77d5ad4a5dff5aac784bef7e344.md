```
define(`confTRY_NULL_MX_LIST',true)
```

The following line states that sendmail will not insert the names and addresses of any local interfaces into the $=w class (list of known “equivalent” addresses):

```
define(`confDONT_PROBE_INTERFACES',true)
```

The next line is the path to the procmail program:

```
define(`PROCMAIL_MAILER_PATH','/usr/bin/procmail')
```

This line tells sendmail to use the sendmail Restricted Shell (smrsh) provided with the distribution instead of /bin/sh for mailing to programs:

```
FEATURE(`smrsh','/usr/sbin/smrsh')
```

This following line defines a table that can be used for customized mail routing:

```
FEATURE(`mailertable','hash -o /etc/mail/mailertable')
```

The next line defines a domain-specific form of aliasing, allowing multiple virtual domains to be hosted on one machine:

```
FEATURE(`virtusertable','hash -o /etc/mail/virtusertable')
```

The following line causes sendmail to reject all mail addressed to address. REDIRECT with a 551 User not local; please try <address> message. If this is set, you can alias people who have left to their new address with .REDIRECT appended.

```
FEATURE(redirect)
```

The next line causes sendmail to always append the domain name to addresses, even with local mail.

```
FEATURE(always_add_domain)
```

This line enables the feature to use the local sendmail.cw file.

```
FEATURE(use_cw_file)
```

This line causes sendmail to use procmail as the local mail handler.

```
FEATURE(local_procmail)
```

This line is an interface to procmail to be used with a mailer table.

```
MAILER(procmail)
```
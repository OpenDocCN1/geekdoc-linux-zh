# 786

# Exit Status

When you specify the -e option, the exit values are returned:

+   - 0 Mail was found.
- >0 Mail was not found or an error occurred.

Otherwise, the following exit values are returned:

+   - 0 Successful completion. Note that this status implies that all messages were sent, but it gives no assurances that any of them were actually delivered.
- >0 An error occurred.

# Files

```
$HOME/.mailrc
  Personal startup file.
$HOME/.mbox  Secondary storage file.
$HOME/.mailock
  Lock file to prevent multiple writers of system mailbox.
/etc/mail/mailx.rc
  Optional system startup file for mailx only.
/etc/mail/Mail.rc
  BSD compatibility systemwide startup file for /usr/ucb/mail and
/tmp/R[emqs]*
  Temporary files.
/usr/share/lib/mailx/mailx.help*
  Help message files.
/var/mail/*  Post office directory.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNWcsu |

# See Also

echo(1), ed(1), ex(1), fmt(1), lp(1), ls(1), mailx(1), mailcompat(1),
more(1), newaliases(1), pg(1), sh(1), vacation(1), vi(1), biff(1B),
uucp(1C), sendmail(1M), aliases(4), passwd(4), attributes(5), environ(5),
largefile(5), standards(5)
# Listing 12-4 The /etc/syslog.conf file

```
/etc/syslog.conf
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
#kern.*								/dev/console

# Log anything (except mail) of level
# info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none	/var/log/messages

# The authpriv file has restricted access.
authpriv.*					/var/log/secure

# Log all the mail messages in one place.
mail.*						/var/log/maillog

# Everybody gets emergency messages,
# plus log them on another machine.
*.emerg						*

# Save mail and news errors of level
# err and higher in a special file.
uucp,news.crit				/var/log/spooler

# Save boot messages also to boot.log
local7.*						/var/log/boot.log
```

There are two important lines (as far as Apache is concerned) in this listing. They are:

```
*.info;mail.none;authpriv.none	/var/log/messages
*.emerg						*
```

The first line tells syslog to write all messages of the info type (except for mail and private authentication) to the /var/log/messages file, and the second line states that all emergency messages should be written to all
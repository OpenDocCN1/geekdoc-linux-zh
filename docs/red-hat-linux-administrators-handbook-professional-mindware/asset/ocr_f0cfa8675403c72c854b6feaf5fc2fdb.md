# ## Configuring syslog

Typically, syslog is already configured on most systems. The default Red Hat installation installs syslog and its /etc/syslog.conf configuration file, which is shown in Listing 6-2.

# **Listing 6-2**  *The syslog configuration file, /etc/syslog.conf*

```
# Log all kernel messages to the console.
# Logging much else clutters up the screen.
kernel.* /dev/console

# Log anything (except mail) of level info or higher.
# Don't log private authentication messages!
*.info;mail.none;authpriv.none /var/log/messages

# The authpriv file has restricted access.
authpriv.* /var/log/secure

# Log all the mail messages in one place.
mail.* /var/log/maillog

# Everybody gets emergency messages.
*.emerg *

# Save mail and news errors of level err and
#higher in a special file.
uucp,news.crit /var/log/spooler
```

The configuration file is quite simple. The blank lines and the lines starting with # are ignored. The structure of a syslog configuration line is as follows:

```
facility.priority destination
```

where *facility* can be one of the following keywords: auth, Authpriv, cron, daemon, kern, lpr, mail, news, syslog, user, uucp, and local0 through local7. A *priority* can be one of the following keywords, in ascending order of severity: debug, info, notice, warning, err, crit, alert, emerg,
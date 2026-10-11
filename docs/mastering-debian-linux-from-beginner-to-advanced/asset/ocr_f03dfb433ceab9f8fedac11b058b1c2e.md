Facilities:

+   - auth, authpriv, cron, daemon, kern, lpr, mail, mark, news, syslog, user, uucp, local0 through local7

Severity levels (from highest to lowest):

+   - emerg, alert, crit, err, warning, notice, info, debug

# Rsyslog Configuration

Debian uses rsyslog as its default syslog daemon. The main configuration file is `/etc/rsyslog.conf`.

Key configuration sections:

+   1. **Modules:** Load required modules for extended functionality.
+   2. **Global directives:** Set global options for rsyslog.
+   3. **Rules:** Define how messages are processed based on facility and severity.

Example rule:

```
auth,authpriv.* /var/log/auth.log
```

This rule sends all auth and authpriv messages to `/var/log/auth.log`.

# Customizing Syslog Rules

To create custom syslog rules:

+   1. Create a new configuration file in `/etc/rsyslog.d/:`
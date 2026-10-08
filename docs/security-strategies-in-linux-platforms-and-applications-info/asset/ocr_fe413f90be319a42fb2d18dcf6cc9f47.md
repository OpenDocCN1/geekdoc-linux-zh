# CHAPTER 4 | User Privileges and Permissions

require the ability to write to that directory. users do not have the ability to overwrite or delete files written by other users.

While other users may be able to read what is written to /tmp, they won't be to delete or overwrite those files. If you want to set the sticky bit on a different directory, the chmod command can help. The following command sets the sticky bit on the /newtmp directory:

```
# chmod o+t /newtmp
```

Alternatively, the following command sets the sticky bit with read, write, and execute permissions for all users on the /newtmp directory:

```
# chmod 1777 /newtmp
```

# Tracking Access Logs

Linux supports logging for services and the kernel. Until recently, this was configured in two different service daemons, syslog and klog, in the /sbin/ directory. The latest versions of Linux include a successor, the /sbin/rslog daemon. The functionality has not changed. The system and kernel logs are intertwined, they're usually part of the same package, rsyslog or syslog. Ubuntu and Red Hat take different approaches to logging configurations from this file.

This section focuses on tracking access—that is, finding those logs record login attempts and especially login failures. These services classify log messages in a number of areas. The relevant areas are auth and authpriv. In the language of the log-service configuration files, auth and authpriv are known as "facilities." While both transmit the same messages, the authpriv facility is normally associated with a more secure file.

This section addresses the basics of tracking access through logs. If you're an administrator for multiple systems, however you may prefer a system that sends you an alert when something goes wrong. That's a log-monitoring system. One option for monitoring is the logwatch log analyzer service, described in Chapter 12.

# Authorization Log Options

Many Linux distributions are in transition from syslog to the rsyslog package. The main syslog configuration file is /etc/syslog.conf. The main configuration file from the /rsyslog package package is /etc/rsyslog.conf. On Ubuntu, it refers to the 50-default.conf file in /etc/rsyslog.d/

Despite the changes to the names and locations of the configuration files, the basic directives have changed. Specifically, for Debian-based systems direct sends information on login attempts to the /var/log/auth.log file:

+   auth, authpriv. * /var/log/auth.log

For Red-Hat systems, the following directive sends information on login attempts de to the /var/log/secure file:

+   authpriv* /var/log/secure

![](bbox=[0.953, 0.583, 0.995, 0.733])
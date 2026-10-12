(off by default) and /etc/httpd/conf/magic (on by default) files to determine the contents of a requested file. Here are the directives that cause that module to be used:

```
<IfModule mod_mime_magic.c>
    # MIMEMagicFile /usr/share/magic.mime
    MIMEMagicFile conf/magic
</IfModule>
```

# ## Setting host name lookups

With the Apache Web server, you can have the server look up addresses for incoming client requests. Turning on the HostnameLookups entry can do this:

```
# HostnameLookups: Log the names of clients or just their IP addresses
HostnameLookups Off
```

If the HostnameLookups directive is turned on, every incoming connection will generate a DNS lookup to translate the client’s IP address into a host name. If your site receives many requests, the server’s response time could be adversely affected. The HostnameLookups should be turned off unless you use a log file analysis program or statistics package that requires fully qualified domain names and cannot perform the lookups on its own. The logresolve program that is installed with the Apache distribution can be scheduled to edit log files by performing host name lookups during off-peak hours.

# ## Configuring HTTP logging

You can set several values related to logging of Apache information. When a relative path name is shown, the /etc/httpd directory is appended (for example, /etc/httpd/logs/error_log). As shown in the following example, you can set the location of error logs, the level of log warnings, and some log nicknames:

```
#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here. If you *do* define an error logfile for a <VirtualHost>
# container, that host’s errors will be logged there and not here.
#
ErrorLog logs/error_log

#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel warn
```
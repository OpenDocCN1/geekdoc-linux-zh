# **Configuring HTTP Logging**

You can set several values related to logging of Apache information. When a relative path-name is shown, the directory set by `ServerRoot` (*/etc/httpd/* by default) is appended (e.g., */etc/httpd/logs/error_log*). As shown in the following example, you can set the location of error logs, the level of log warnings, and some log nicknames:

```
#
# ErrorLog: The location of the error log file.
# If you do not specify an ErrorLog directive within a <VirtualHost>
# container, error messages relating to that virtual host will be
# logged here. If you *do* define an error log file for a <VirtualHost>
# container, that host's errors will be logged there and not here.
#
ErrorLog logs/error_log
#
# LogLevel: Control the number of messages logged to the error_log.
# Possible values include: debug, info, notice, warn, error, crit,
# alert, emerg.
#
LogLevel warn

#
# The following directives define some format nicknames for use with
# a CustomLog directive (see below).
#
LogFormat "%h %l %u %t "%r" %>s %b" "%{Referer}i\"\"%{User-Agent}i\"\"" combined
LogFormat "%h %l %u %t "%r" %>s %b" common
LogFormat "%{Referer}i -> %I" referer
LogFormat "%{User-agent}i" agent.

#
# Location and format of the access logfile (Common Logfile Format).
# If you do not define any access logfiles within a <VirtualHost>
# container, they will be logged here.  Contrariwise, if you *do*
# define per-<VirtualHost> access logfiles, transactions will be
# logged therein and *not* in this file.
#
# CustomLog logs/access_log common

# If you would like to have separate agent and referer logfiles,
# uncomment the following directives.

#
#CustomLog logs/referer_log referer
#CustomLog logs/agent_log agent
```
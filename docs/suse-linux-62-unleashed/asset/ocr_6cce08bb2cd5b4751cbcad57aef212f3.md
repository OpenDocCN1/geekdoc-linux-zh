# Networking and Internet Services
PART II

# LISTING 11.2 CONTINUED

```
# ScoreBoardFile: File used to store internal server process information.
# Not all architectures require this. But if yours does (you'll know because
# this file will be created when you run Apache) then you *must* ensure that
# no two invocations of Apache share the same scoreboard file.

ScoreBoardFile /var/log/httpd.apache_runtime_status

# In the standard configuration, the server will process this file,
# srm.conf, and access.conf in that order. The latter two files are
# now distributed empty, as it is recommended that all directives
# be kept in a single file for simplicity. The commented-out values
# below are the built-in defaults. You can have the server ignore
# these files altogether by using /dev/null/ (for Unix) or
# 'nul' (for Win32) for the arguments to the directives.

#ResourceConfig conf/srm.conf
#AccessConfig conf/access.conf

# Timeout: The number of seconds before receives and sends time out.

Timeout 300

# KeepAlive: Whether or not to allow persistent connections (more
# one request per connection). Set to "Off" to deactivate.

KeepAlive On

# MaxAliveRequests: The maximum number of requests to allow
# during a persistent connection. Set to 0 to allow an unlimited amount.
# We recommend you leave this number high, for maximum performance.

MaxAliveRequests 100

# KeepAliveTimeout: Number of seconds to wait for the next request from the
# same client on the same connection.

KeepAliveTimeout 15
```
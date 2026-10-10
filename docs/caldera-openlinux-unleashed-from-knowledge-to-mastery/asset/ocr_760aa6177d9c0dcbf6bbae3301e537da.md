# **Tip**

If you are hosting Web sites on an Intranet or internal network, there is often a chance that users will use the shortened name of the machine rather than the fully qualified domain name. For example, they might type `http://bugserver/index.html` in their browser location field, rather than `http://bugserver.database.com/index.html`. In that case, Apache will not recognize that those two addresses should go to the same virtual host. You could get around this by setting up `VirtualHost` directives for both `bugserver` and `bugserver.database.com`, but the easy way around this is to use the `ServerAlias` directive, which lists all valid aliases for the machine:

```
```
ServerAlias bugserver
```
```

# **Caution**

If you plan to run a large number of virtual hosts on your system, you should consider sending all logged information to the standard Apache log files instead of to individual files. The reason is that you may reach your system's file descriptor limit because you would be consuming one file descriptor per log file. The system per process limit is 1024 in Linux 2.2, but may be much lower due to `ulimit` restrictions. Symptoms of this problem include error messages such as "unable to fork()," "no information being written to the log files," or "poor response to HTTP requests."

# ## Logging

Apache provides for logging just about any information you might be interested in from Web accesses. Two standard log files are generated when you run your Apache server—`access_log` and `error_log`. All logs except for the `error_log` (by default, this is just the `access_log`) are generated in a format specified by the `CustomLog` and `LogFormat` directives. These directives appear in your `httpd.conf` file.

A new log format can be defined with the `LogFormat` directive:

```
```
LogFormat " %h %1 %u %t "%r" %>s %b" common
```
```

The common log format is a good starting place for creating your own custom log formats. Note that most of the log analysis tools available will assume that you are using the common log format or the combined log format, both of which are defined in the default configuration files.
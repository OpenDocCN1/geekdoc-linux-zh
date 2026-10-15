| Field Specifier | Description |
|---|---|
| %a | Remote IP address |
| %A | Local IP address |
| %b | Bytes sent, excluding HTTP headers |
| %{variable}e: | The contents of the environment variable |
| %f | Filename |
| %h | Remote host |
| %l | Remote logname (from identd, if supplied) |
| %m | The request method |
| %P | The process ID of the child that serviced the request |
| %r | First line of request |
| %s | Status |
| %t | Time, in Common Log Format time format (standard English format) |
| %u | Remote user (from auth; may be bogus if return status (%s) is 401) |
| %U | The URL path requested |
| %v | The canonical ServerName of the server serving the request |

# TABLE 22-11 Apache Log Field Specifiers

# Generating and Managing Log Files

Instead of maintaining one large log file, you can create several log files using the CustomLog or TransferLog directive. This is helpful for virtual hosts where you may want to maintain a separate log file for each host. You use the FormatLog directive to define a default format for log records. The TransferLog then uses this default as its format when creating a new log file. CustomLog combines both operations, enabling you to create a new file and to define a format for it.

```
FormatLog "%h %l %u %t \"%r\"" %s %b
# Create a new log file called myprojlog using the FormatLog format
TransferLog myprojlog
# Create a new log file called mypicslog using its own format
CustomLog mypicslog "%h %l %u %t \"%r\"" %s %b
```

Apache provides two utilities for processing and managing log files. logresolve resolves IP addresses in your log file to hostnames. rotatelogs rotates log files without having to kill the server. You can specify the rotation time.

> NOTE The Apache Web server can also provide detailed reports on server activity and configuration, letting you display this information to remote servers. The Location directive server-info will display the configuration details of your Web server, and the server-status directive will show Web processes. The pages server-info and server-status will display the reports, as in http://localhost/server-info. Use the ExtendedStatus directive to enable detailed reports.
bugserver.gnuix.org, but the easy way around it is to use the `ServerAlias` directive, which lists all valid aliases for the machine:

```
ServerAlias bugserver
```

For more information about `VirtualHost`, refer to the help system on http://localhost/manual.

# # Logging

Apache provides for logging just about any web access information you might be interested in. Logging can help with

+   - System resource management, by tracking usage
+   - Intrusion detection, by documenting bad HTTP requests
+   - Diagnostics, by recording errors in processing requests

Two standard log files are generated when you run your Apache server: `access_log` and `error_log`. They are found under the `/var/log/httpd` directory. (Others include the SSL logs `ssl_access_log`, `ssl_error_log`, and `ssl_request_log`.) All logs except for the `error_log` (by default, this is just the `access_log`) are generated in a format specified by the `CustomLog` and `LogFormat` directives. These directives appear in your httpd.conf file.

A new log format can be defined with the `LogFormat` directive:

```
```
LogFormat "%h %l %u %t "%r" %>s %b" common
```
```

The common log format is a good starting place for creating your own custom log formats. Note that most of the available log analysis tools assume you're using the common log format or the combined log format-both of which are defined in the default configuration files.

The following variables are available for `LogFormat` statements:

+   - `%a`	Remote IP address.
+   - `%A`	Local IP address.
+   - `%b`	Bytes sent, excluding HTTP headers. This is shown in Apache's Combined Log Format (CLF). For a request without any data content, a `-` is shown instead of `0`.
+   - `%B`	Bytes sent, excluding HTTP headers.
+   - `%(VARIABLE)e`	The contents of the environment variable VARIABLE.
+   - `%f`	The filename of the output log.
+   - `%h`	Remote host.
+   - `%H`	Request protocol.
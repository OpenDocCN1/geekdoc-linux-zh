Many more directives control the way that the Apache Web server works. The following list summarizes some of the directives you can use in the httpd.conf file. You can leave most of these directives in their default settings, but it's important to know about them if you're maintaining a Web server.

+   - **Listen IP-Address:Port** — Forces the Web server to listen to a specific IP address and port number. By default, the Web server responds to all IP addresses associated with the host.
+   - **User name [ #id ]** — Specifies the user name (or ID) the HTTP daemon uses. You can leave this directive at the default setting (apache). If you specify a user ID, use a hash (#) prefix for the numeric ID.
+   - **Group name [ #id ]** — Specifies the group name (or ID) of the HTTP daemon when running in standalone mode. The default group name is apache.
+   - **ServerRoot pathname** — Specifies the directory where the Web server is located. By default, the configuration and log files are expected to reside in subdirectories of this directory. In Red Hat Linux, ServerRoot is set to /etc/httpd.
+   - **ServerName www.company.com:80** — Sets the server's host name to www.company.com and the port number to 80. ServerName is used only when redirecting a Web page to another.
+   - **StartServers num** — Sets the number of child processes that start as soon as the Apache Web server runs. The default value is 8.
+   - **MaxSpareServers num** — Sets the desired maximum number of idle child-server processes (a child process is considered idle if it's not handling an HTTP request). The default value is 20.
+   - **MinSpareServers num** — Sets the desired minimum number of idle child-server processes (a child process is considered idle if it's not handling an HTTP request). A new spare process is created every second if the number falls below this threshold. The default value is 5.
+   - **Timeout numsec** — Sets the number of seconds that the server waits for a client to send a query after the client establishes connection. The default timeout is 300 seconds (five minutes).
+   - **ErrorLog filename** — Sets the file where httpd logs the errors it encounters. If the filename does not begin with a slash (/), the name is taken to be relative to ServerRoot. The default ErrorLog is /etc/httpd/logs/error_log, but /etc/httpd/logs is a symbolic link to the /var/log/httpd directory. Therefore the log files are in the /var/log/httpd directory. Typical error-log entries include events such as server restarts and any warning messages, such as the following:

```
[Sun Jul 13 14:10:34 2003] [notice] Apache/2.0.45 (Red Hat Linux) configured -- resuming normal operations
[Sun Jul 13 15:47:03 2003] [error] [client 192.168.0.2] File does not exist: /var/www/html/sample.html
```
# #626 Configuring the Apache Web Server

+   * **StartServers num**: Sets the number of child processes that start as soon as the Apache Web server runs. The default value is 8.
* **MaxSpareServers num**: Sets the desired maximum number of idle childserver processes (a process is considered idle if it's not handling an HTTP request). The default value is 20.
* **MinSpareServers num**: Sets the desired minimum number of idle child processes (a process is considered idle if it's not handling an HTTP request). A new process is created every second if the number falls below this threshold. The default value is 5.
* **Timeout sec**: Sets the number of seconds that the server waits for a client to send any other connection. The default Timeout is 300 seconds (five minutes).
* **ErrorLog filename**: Sets the file where httpd logs the errors encounters. If the filename does not begin with a slash (/), it is taken to be relative to ServerRoot. The default ErrorLog is /etc/httpd/error_log a symbolic link to /var/log/httpd directory. Therefore the log files include events, such as server restarts, and any other messages, show the following:

+   * **TransferLog filename**: Sets the file where httpd records all client accesses (including failed accesses). The default TransferLog is /var/log/httpd/access_log. The following shows how a typical access record is recorded in the log file:
```
[Mar 13 18:10:01 2004] [notice] Apache/2.0.48 (fedora) configured - resuming normal operations
[Mar 13 18:10:37 2004] [client 192.168.0.3] File does not exist: /var/www/htd//
```

```
192.168.0.3 - [Mar 13 18:10:23 2004] -000 "GET / HTTP/1.1" 200 3888 - "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; (RI: 1.3))"
192.168.0.3 - [Mar 13 18:10:23 2004] -000 "GET /icons/apache_pb2.gif HTTP/1.1" 404 2414 - "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; (RI: 1.3))_NET CL 1.4322"
192.168.0.3 - [Mar 13 18:10:23 2004] -000 "GET / HTTP/1.1" 200 2243 - "http://192.168.0.6/" "Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; (RI: 1.3))_NET CL 1.41327"
```

+   * **LogFormat formatname**: Specifies the format of log file entries for the TransferLog. The CustomLog directive also uses this format to produce logs in a specific format.
* **CustomLog filename**: Sets the name of the custom log file where httpd records all client accesses (including failed accesses) in a format specified by formatname (which you define using a LogFormat)
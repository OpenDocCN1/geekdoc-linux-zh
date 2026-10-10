
## TABLE 20-7 (continued)

| Argument | Description |
| :--- | :--- |
| **-f** *file* | Uses *file* as the ServerConfigFile directive, rather than the default of /etc/httpd/conf/httpd.conf. |
| **-h** | Displays a list of possible command-line arguments. |
| **-l** | Lists the modules linked into the executable at compile time. |
| **-L** | Prints a verbose list of directives that can be used in the configuration files, along with a short description and the module that contains each directive. |
| **-S** | Lists the configured settings for virtual hosts. |
| **-t** | Performs a syntax check on the configuration files. The results will either be Syntax OK or an error notification, for example, Syntax error on line 118 of /etc/httpd/conf/httpd.conf. |
| **-T** | Same as -t, except that there is no check of the DocumentRoot value. |
| **-v** | Prints the version information:<br>Server version: Apache/2.2.8 (Unix)<br>Server built: Feb 25 2008 07:05:32 |
| **-V** | Lists the version information and any values defined during compilation:<br>Server version: Apache/2.2.8 (Unix)<br>Server built: Feb 25 2008 07:05:32<br>Server's Module Magic Number: 20051115:11<br>Architecture: 32-bit<br>....<br>Server compiled with....<br> -D APACHE_MPM_DIR="server/mpm/prefork"<br> -D APR_HAS_MMAP<br> -D APR_HAVE_IPV6 (IPv4-mapped addresses enabled)<br> .<br> .<br> .<br> -D SERVER_CONFIG_FILE="conf/httpd.conf" |
| **-k** *option* | Uses *-k* with the start, stop, restart, graceful, or graceful-stop options to change the current state of the Web Server. |

## Monitoring Server Activities

An Apache Web Server is a tempting target for someone with a desire to hijack a computer for bad purposes. There are many techniques you can use to secure your server (covered in Chapter 13), which range from SELinux to using certificates to controlling how scripts are run. Described here, however, are techniques for keeping an eye on the performance and security of your Apache Web Server. Watching your server carefully can often stop an attack before it gets anywhere.

Apache provides two unique built-in methods to check the performance and status of your Web Server. The server-status handler can be configured to show information about server processes. The server-info handler can be configured to display a detailed summary of the Web Server's configuration. You can activate these services by adding the following lines to the `/etc/httpd/conf/httpd.conf` file:

```
<Location /server-status>
    SetHandler server-status
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>

<Location /server-info>
    SetHandler server-info
    Order deny,allow
    Deny from all
    Allow from 127.0.0.1
</Location>
```

In this example, all users from the local computer can display the server-info and server-status pages. You can change `127.0.0.1` to the name of any domain or host that your Apache server is hosting.

### Displaying Server Information

The Server Information (server-info) page contains the server version information and various general configuration parameters and breaks up the rest of the data by module. Each loaded module is listed, with information about all directives supported by that module, and the current value of any defined directives from that module.

The Server Information is usually quite verbose and contains much more information than can be displayed in Figure 20-3, which shows only the links to each module’s section and the general Server Settings section.

### Displaying Server Status

The contents of the server-status page include version information for the server, the current time, a time stamp of when the server was last started, and the server’s uptime. The page also details the status of each server process, choosing from several possible states (waiting for a connection, just starting up, reading a request, sending a reply, waiting to read a request before reaching the number of seconds defined in the `KeepAliveTimeout`, performing a DNS lookup, logging a transaction, or gracefully exiting).

## Setting Up a Web Server

## 20

### FIGURE 20-3

The server-info page displays server and module information.

![](img/2f265415ceec72538dd3c78ffca75c10_842_0.png)

The bottom of the server-status page lists each server by process ID (PID) and indicates its state, using the same possible values. Figure 20-4 shows an example of this page.

The server-status page can also perform automatic updates to provide even closer monitoring of the server. If the URL http://localhost/server-status?refresh=40 is specified, the server-status page displayed in your browser will be updated every 40 seconds. This enables a browser window to be entirely devoted to continually monitoring the activities of the Web Server.

By default, only basic status information is generated. If you would like to generate full status information, you need to turn on the ExtendedStatus directive by uncommenting the last line in the following code:

```
# ExtendedStatus: controls whether Apache will generate "full" status
# information (ExtendedStatus On) or basic information (ExtendedStatus
# Off) when the "server-status" handler is called. The default is Off.
#
#ExtendedStatus On
```

### FIGURE 20-4

The Apache server-status page displays general Apache information and reports on individual server process activities.

![](img/2f265415ceec72538dd3c78ffca75c10_843_0.png)

### Further Security of Server-Info and Server-Status

Because both the server-info and server-status pages contain private information that should not be accessible to just anyone on the network, there are a few extra ways you can secure that information. You can restrict that information only to the local host, however, in some environments that may not be practical.

If you must allow other machines or networks access to such detailed configuration information, allow only as many machines as is necessary, and preferably only those machines on your local network. Also, be aware that, in the wrong hands, the information displayed by the server-info and server-status pages can make it much easier for the security of your entire machine to be compromised.

It may also be beneficial to change the URL used to reference both of the aforementioned pages. This is an example of “security through obscurity,” which should not be relied on but which can make it just a little more difficult for unauthorized individuals to obtain information about your Web server's configuration (particularly if you cannot restrict such connections to the local network). To accomplish this, simply change the filename in the Location directive, as in the following lines:

```
<Location /server.information.page>
```

and:

```
<Location /server.status.page>
```

### Logging Errors

The error log contains messages generated by the server that describe various error conditions. The ErrorLog and LogLevel directives in the httpd.conf file (as described in the section on configuring the server) can modify the filename and the amount of information that is logged. The default file is /etc/httpd/logs/error_log (which is a link to /var/log/httpd/error_log). Here are a few sample lines from the error log:

```
[Mon Feb 16 05:13:41 2009] [notice] Apache/2.2.3 (CentOS)
configured -- resuming normal operations
[Mon Feb 16 05:13:46 2009] [error] [client 127.0.0.1] client denied by server configuration: /var/www/html/server-info
[Mon Feb 16 05:13:53 2009] [error] [client 127.0.0.1] File does not exist:
/var/www/html/favicon.ico
[Mon Feb 16 05:15:44 2009] [notice] caught SIGTERM, shutting down
```

The first line indicates that the server has just been started and will be logged regardless of the LogLevel directive. The second line indicates an error that was logged to demonstrate a denied request. The third line shows an error, which represents a request for a file that does not exist. The fourth line, also logged regardless of the LogLevel directive, indicates that the server is shutting down. The error log should also be monitored periodically because it will contain the error messages from CGI scripts that might need repair.

### Logging Hits

Every incoming HTTP request generates an entry in the transfer log (by default, /etc/httpd/logs/access_log, which is a link to /var/log/httpd/access_log). Statistics packages and log file analysis programs typically use this file because manually reading through it can be a rather tedious exercise. (See the information on the logwatch facility in Chapter 13.)

The format of the transfer log can be altered by the LogFormat and CustomLog directives in the httpd.conf file, as described in the “Configuring the Web Server (httpd.conf)” section. If you attempted to access http://localhost/ following the installation procedure (from Figure 20-1), the following lines (in the “common” format) would be written to the access_log:

```
127.0.0.1 - - [16/Feb/2009:05:21:16 -0500] "GET / HTTP/1.1" 403 5043 "-"
"Mozilla/5.0 (X11; U: Linux i686; en-US; rv:1.9b5) Gecko/2008052519
```

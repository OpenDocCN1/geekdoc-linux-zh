
## Configuring the Apache Server

Now that your Web server is working (or, at least, I hope it is), step through the next section. It helps you understand how to set up more complex Web server arrangements and protect your server from misuse. Stepping through that section will also help you troubleshoot your Web server, in case it isn't working.

> **TIP:** If your Web server is accessible from your local host but not available to others from your LAN or the Internet, you may need to change your firewall rules to allow greater access. Appendix B explains how to make your Web server or other server services accessible. In particular, you need to open tcp port 80 and possibly tcp port 443 (if you offer https content). Also, if SELinux is enabled, it may prevent access to your Web server that you might otherwise expect to work. To disable SELinux, type `setenforce 0` as root. Or type `man httpd_selinux` to learn how to use SELinux with httpd. In particular, make sure that all booleans are set properly to allow the services you want and that all file context labels are correct for your content and configuration files.

The primary file for configuring your Apache Web server is `httpd.conf` (located in the `/etc/httpd/conf` directory). A few years ago, the Apache project began recommending not using additional configuration files, such as `srm.conf` and `access.conf`, and simply putting everything in `httpd.conf`. In recent releases, however, there has been a trend toward having modules and other components that are used with Apache to have their own configuration files (usually located in the `/etc/httpd/conf.d/` directory).

All Apache configuration files are plain-text files and can be edited with your favorite text editor. The `/etc/httpd/conf/httpd.conf` file is reproduced in its entirety in the following section, with explanations inserted after related blocks of options (intended to supplement the comments provided with each file).

Some individual modules, scripts, and other services related to Apache, such as perl, php, ssl, and webalizer, have individual configuration files that may interest you. Those files are contained in the `/etc/httpd/conf.d/` directory. See the "Configuring Modules and Related Services (`/etc/httpd/conf.d/*.conf`)" section later in this chapter.

> **NOTE:** More information on Apache can be obtained on your own Web server, from `http://localhost/manual/` (if the `httpd-manual` package is installed).

### Configuring the Web server (httpd.conf)

The `httpd.conf` file, the primary configuration file for the Apache Web server, contains options that pertain to the general operation of the server. The default filename (`/etc/httpd/conf/httpd.conf`) can be overridden by the `-f filename` command-line argument to the httpd daemon or the `ServerConfigFile` directive. The following sections list the contents of the `httpd.conf` file and describe how to use the file.

The first section contains comments about the `httpd.conf` file:

```apache
# This is the main Apache server configuration file. It contains the
# configuration directives that give the server its instructions.
# See <URL:http://httpd.apache.org/docs/2.2/> for detailed information.
# In particular, see
# <URL:http://httpd.apache.org/docs/2.2/mod/directives.html>
# for a discussion of each configuration directive.
#
# Do NOT simply read the instructions in here without understanding
# what they do. They're here only as hints or reminders. If you are
# unsure consult the online docs. You have been warned.

.
.
.
```

This section consists entirely of comments. It basically tells you how information is grouped in this file and how the httpd daemon accesses this file. By default, log files are in the /var/log/httpd directory.

### Setting the global environment

In “Section 1: Global Environment” of the httpd.conf file, you set directives that affect the general workings of the Apache server. Most of the global directives can be overridden for specific virtual domains, if you are providing Web service for more than one domain. Here is what the different directives are for:

```apache
### Section 1: Global Environment
#
# The directives in this section affect overall operation of Apache,
# such as the number of concurrent requests it can handle or where it
# can find its configuration files.
#
```

### Revealing subcomponents

The ServerTokens directive lets you prevent remote computers from finding out what subcomponents you are running on your Apache server. Comment out this directive if you don’t mind exposing this information. To prevent exposure, ServerTokens is set as follows:

```apache
#
# Don't give away too much information about all the subcomponents
# we are running. Comment out this line if you don't mind remote sites
# finding out what major optional modules you are running
ServerTokens OS
```

Setting ServerTokens to ProductOnly will minimize the connection information a potential cracker could see.

### Setting the server root directory

The `ServerRoot` directive specifies the directory that contains the configuration files, a link to the log file directory, and a link to the module directory. An alternative `ServerRoot` path name can be specified using the -d command-line argument to httpd.

```apache
ServerRoot "/etc/httpd"
```

### Storing the server’s PID file

The Apache Web server keeps track of the PID for the running server process. You can change the locations of this file using the entry following:

```apache
PidFile run/httpd.pid
```

Apache uses the `PidFile` to store the process ID of the first (root-owned) master daemon process. This information is used by the `/etc/init.d/httpd` script when shutting down the server and also by the server-status handler (as described later in this chapter).

### Configuring timeout values

You can set several values that relate to timeout. Some of these values are described in the text following the code:

```apache
Timeout 120
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
```

The `Timeout` directive determines the number of seconds that Apache will hold a connection open between the receipt of packets, between the receipt of acknowledgements on sent responses, or while receiving an incoming request. The default of two minutes (120 seconds) can be reduced if you find an excessive number of open, idle connections on your machine.

The `KeepAlive` directive instructs Apache to hold a connection open for a period of time after a request has been handled. This enables subsequent requests from the same client to be processed faster, as a new connection doesn’t need to be created for each request.

The `MaxKeepAliveRequests` directive sets a limit on the number of requests that can be handled with one open connection. The default value is certainly reasonable because most connections will hit the `KeepAliveTimeout` before `MaxKeepAliveRequests`.

The `KeepAliveTimeout` directive specifies the number of seconds to hold the connection while awaiting another request. You might want to increase the default (15 seconds). Reasons for having a longer timeout could be to allow all the images on the page to be downloaded on the same connection or to take into account how long it may take a client to peruse your average page and select a link from it. The Web application you are using may also need a longer persistent connection. (Of course, a longer `KeepAliveTimeout` prevents each server from moving on to another client during this time period, so you may find that you need to add more request processes to account for that.)

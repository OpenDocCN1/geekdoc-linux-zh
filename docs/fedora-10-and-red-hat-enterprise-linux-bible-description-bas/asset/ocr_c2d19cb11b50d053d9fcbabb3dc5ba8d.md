# Chapter 21: Setting Up a Web Server

CROSS-REFERENCE: More information on Apache can be obtained on your own Web server, from http://localhost/manual/ (If the httpd-manual package is installed).

# Configuring the Web server (httpd.conf)

The httpd.conf file is the primary configuration file for the Apache server. It contains options that pertain to the general operation of the server. The default filename (/etc/httpd/conf/httpd.conf) can be overridden by the -f filename argument to the httpd daemon or the ServerConfig directive. The following sections list the contents of the httpd.conf file and describe how to use the file.

The first section contains comments about the httpd.conf file:

```
# This is the main Apache configuration file. It contains the
# configuration directives that give the server its instructions.
# See <URL:http://httpd.apache.org/docs/2.2/> for detailed information.
# In particular, see
# <URL:http://httpd.apache.org/docs/2.2/mod/directives.html>
# for a discussion of each configuration directive.

# Do NOT imply the instructions in here without understanding
# what they do. They're here as hints or reminders. If you are
# unsure consult the online docs. You have been warned.

# The configuration directives are grouped into three basic sections:
# 1. Directories that control the operation of the Apache server
# process as a whole (the 'global environment').
# 2. Directories that define parameters of the main or default server,
# which responds to requests that aren't handled by a virtual host.
# These directives also provide default values for the settings
# of all virtual hosts.
# 3. Settings for virtual hosts, which allow Web requests to be sent
# to different addresses or hostnames and have them handled by
# the Apache server process.
# Configuration and log names: If filenames you specify for
# many of the server's control files begin with "/" or "drive:" for
# Win32, the server will use that explicit path. If the filenames do
# "not" begin with "/", the value of ServerRoot is prepended - so
# "log.foo with ServerRoot set to "usr/local/apache" will be
# interpreted by the server as "usr/local/apache/logs/foo.log".
```

This section consists of interesting comments. It tells you how information is grouped
together in this file and how the httpd daemon accesses this file. By default, log files are in the
/var/log/httpd directory.
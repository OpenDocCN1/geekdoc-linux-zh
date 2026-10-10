
The first line indicates that the server has just been started and will be logged regardless of the LogLevel directive. The second line indicates an error that was logged to demonstrate a denied request. The third line shows an error, which represents a request for a file that does not exist. The fourth line, also logged regardless of the LogLevel directive, indicates that the server is shutting down. The error log should also be monitored periodically because it will contain the error messages from CGI scripts that might need repair.

## Logging hits

Every incoming HTTP request generates an entry in the transfer log (by default, `/etc/httpd/logs/access_log`, which is a link to `/var/log/httpd/access_log`). Statistics packages and log file analysis programs typically use this file because manually reading through it can be a rather tedious exercise. (See the information on Logwatch in Chapter 14.)

The format of the transfer log can be altered by the `LogFormat` and `CustomLog` directives in the `httpd.conf` file, as described in the “Configuring the Web server (httpd.conf)” section. If you attempted to access `http://localhost/` following the installation procedure (from Figure 21-1), the following lines (in the “common” format) would be written to the access_log:

```
127.0.0.1 - - [26/Apr/2008:00:23:33 -0600] "GET / HTTP/1.1" 403 931 "-" "Mozilla/5.0
(X11; U; Linux i686; rv:1.7.3) Gecko/20041002 Firefox/0.10.1"

127.0.0.1 - - [26/Apr/2008:00:23:34 -0600] "GET /icons/apache_pb2.gif HTTP/1.1" 200
2414 "http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; rv:1.7.3)
Gecko/20041002 Firefox/0.10.1"

127.0.0.1 - - [26/Apr/2008:00:23:34 -0600] "GET /icons/powered_by_fedora.png HTTP/1.1"
200 2243 "http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; rv:1.7.3)
Gecko/20041002 Firefox/0.10.1"
```

The Apache Test Page actually is an error condition (403), which indicates that the Apache server is running, but that the administrator of the server hasn’t added a home page yet. The next two lines show the Apache (apache_pb2.gif) and Fedora (powered_by_fedora.png) icons that appear on the test page, respectively, for Fedora. (RHEL systems have a Red Hat icon.)

Viewing the server-info and server-status pages (as shown in Figures 21-3 and 21-4, respectively) generated the following entries:

```
127.0.0.1 - - [26/Apr/2008:23:40:41 -0400] "GET /server-info HTTP/1.1"
200 42632

127.0.0.1 - - [26/Apr/2008:23:41:49 -0400] "GET /server-status
HTTP/1.1" 200 1504
```

The denied attempt to access the server-status page logged the following line (note the 403 server response code):

```
127.0.0.1 - - [26/Apr/2008:23:43:07 -0400] "GET /server-status
HTTP/1.1" 403 211
```

## Analyzing Web-server traffic

The webalizer package can take Apache log files and produce usage reports for your server. Those reports are created in HTML format so you can display the information graphically. Information is produced in both table and graph form.

To use the webalizer command, the webalizer package must be installed (`yum install webalizer`). You can run webalizer with no options and have it take the values in the /etc/webalizer.conf file to get the information it needs. As an alternative, you can use command-line options to override settings in the webalizer.conf file. To use the defaults, simply run the following:

```
# webalizer
```

If all goes well, the command should run for a few moments and exit silently. Based on the information in the /etc/webalizer.conf file, the /var/log/httpd/access_log log file is read and an index.html file is copied to the /var/www/html/usage/ directory. You can view the output by opening the file in any browser window. For example, you could type the following in the location box:

```
http://localhost/usage
```

The output report shows a 12-month summary of Web server activity. On the bar chart, for each month a green bar represents the number of hits on the Web site, a dark blue bar shows the number of different files hit, and a light blue bar shows the number of pages opened. It also shows data for the number of visits and the number of sites that visited in the right column. The amount of data transferred, in kilobytes, is displayed as well.

Figure 21-5 shows an example of a webalizer output file for a Web server that has been running for several months.

Below the chart, a table shows daily and monthly summaries for activity during each month. Users can click the name of a month to see detailed activity.

> **TIP:** Because Webalizer supports both common log format (CLF) and combined log format, it can be used to display information for log files other than those produced for Apache. For example, you could display statistics for your FTP server or Squid server.

Several other software tools are available for analyzing transfer statistics. The accompanying sidebar on statistics packages available for Fedora and Red Hat Enterprise Linux systems describes some of these tools.

![](img/fb202c163797a743c3c6cf236316bc96_917_0.png)

## Statistics Packages Available for Fedora and RHEL

Analyzing the transfer log by hand isn’t much fun. Several packages have been written to automate this task, including the following two:

- **Analog** — This free log-file analyzer is very fast and easily configurable, and it produces very detailed output (including bar graphs and hypertext links). More information can be found at www.analog.cx.
- **AWStats** — The Advanced Web Statistics tool (awstats package) produces graphical statistics representing Web-server access. AWStats can work with log files in the Apache common log format, as well as log files from sendmail, FTP, and other network servers. It can report statistics, such as the number of people who have visited, visits made per person, the domain and country of each visitor, and the number of visits made by robots.

## Summary

Web servers are responsible for storing and delivering the vast amount of content available on the World Wide Web to clients all over the world. Although several Web-server software packages are available for Fedora and RHEL systems, the most popular is by far the Apache Web server.

This chapter describes how to install, configure, and run an Apache server in Fedora. The `httpd` daemon process handles requests for Web content (HTTP). Configuration files define what content is made available and how it can be accessed. In particular, the `/etc/httpd/conf/httpd.conf` file is used to configure the server.

The Apache `httpd` package also includes facilities for logging error and transfer messages. You can look for the `access_log` and `error_log` files in the `/etc/httpd/logs` directory. The `access_log` file contains information on content requests that have been serviced by the server. The `error_log` file lists error conditions that have occurred and times when service has been denied. You can use tools such as Webalizer to simplify the viewing of Apache log data.

# **Chapter 22
Setting Up an LDAP
Address Book Server**

**In This Chapter**

- Understanding LDAP
  - Using OpenLDAP
  - Configuring an LDAP server
  - Creating an LDAP address book
  - Using Thunderbird to access the address book

Sometimes an organization needs a convenient way to gather, store, and distribute information for access by the applications that need it. The Lightweight Directory Access Protocol (LDAP) simplifies the process of creating and using directories of information by network-ready applications.

The intention of LDAP is to simplify the overhead needed to provide directory services described in the X.500 specification. LDAP is a subset of X.500 features. By standardizing the structure of database information, LDAP can get around proprietary storage formats to allow many different applications to share the same data.

> **NOTE:** X.500 is a CCITT specification that has become part of the Open Systems Interconnection (OSI) standards that define a layered framework for interconnecting networks and related services. With the dominance of TCP/IP networks (such as the Internet) in the world, OSI never became the predominant network framework that some expected it to be. Despite that, the seven-layer OSI reference model is often used in classrooms to teach networking theory. Likewise, some of these specifications, such as X.500, have been *adopted* (and sometimes *adapted*) where standard, cross-platform features are required.

Fedora and RHEL systems include OpenLDAP software packages to implement LDAP server and client services. To illustrate how to configure and use an LDAP server with OpenLDAP, and make it accessible to user applications, this chapter goes through the process of setting up a shared address book to run on a Fedora or RHEL system. It also describes how to use e-mail clients that can access the LDAP address book.

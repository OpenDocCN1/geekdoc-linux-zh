
CentOS5.0-beta5.6.e15.centos Firefox/3.0b5" 127.0.0.1 - [12/Feb/2009:05:21:16 -0500] "GET /icons/apache_pb.gif HTTP/1.1" 200 2326 "http://localhost/" "Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9b5) Gecko/2008052519 CentOS/5.0b5-0.beta5.6.e15.centos Firefox/3.0b5" 127.0.0.1 - - [12/Feb/2009:05:21:16 -0500] "GET /icons/powered_by_rh.png HTTP/1.1" 200 1213 "http://localhost/" "Mozilla/5.0 ; Linux i686; en-US; rv:1.9b5) Gecko/200805219 CentOS5.0-beta5.6.e15.centos Firefox/3.0b5" 

The Apache Test Page actually is an error condition (403), which indicates that the Apache server is running, but that the administrator of the server hasn't added a home page yet. The next two lines show the Apache (apache_pb.gif) and CentOS (powered_by_rh.png) icons that appear on the test page, respectively, for CentOS.

## Analyzing Web-Server Traffic

The *webalizer* package can take Apache log files and produce usage reports for your server. Those reports are created in HTML format so you can display the information graphically. Information is produced in both table and graph form.

To use the *webalizer* command, the *webalizer* package must be installed (type **yum install webalizer**). You can Run Webalizer with no options and have it take the values in the /etc/webalizer.conf files to get the information it needs. As an alternative, you can use command-line options to override settings in the webalizer.conf file. To use the defaults, simply run the following:

```
# webalizer
```

If all goes well, the command should run for a few moments and exit silently. Based on the information in the /etc/webalizer.conf file, the /var/log/httpd/access_log log file is read and an index.html file is copied to the /var/www/html/Usage/ directory. You can view the output by opening the file in any browser window. For example, you could type the following in the Location box:

```
http://localhost/Usage
```

The output report shows a 12-month summary of Web Server activity. On the bar chart, for each month a green bar represents the number of hits on the web site, a dark blue bar shows the number of different files hit, and a light blue bar shows the number of pages opened. It also shows data for the number of visits and the number of sites that visited in the right column. The amount of data transferred, in kilobytes, is displayed as well.

Figure 20-5 shows an example of a Webalizer output file for a Web Server that has been running for several months.

Below the chart, a table shows daily and monthly summaries for activity during each month. Users can click on the name of a month to see detailed activity.

![](img/2f265415ceec72538dd3c78ffca75c10_846_0.png)

> **TIP** Because Webalizer supports both common log format (CLF) and combined log format, it can be used to display information for log files other than those produced for Apache. For example, you could display statistics for your FTP server or Squid server.

Several other software tools are available for analyzing transfer statistics. The accompanying sidebar on statistics packages available for CentOS systems describes some of these tools.

## Statistics Packages Available for CentOS

Analyzing the transfer log by hand isn't much fun. Several packages have been written to automate this task, including the following two:

- **Anolog** — This free log-file analyzer is very fast and easily configurable, and it produces very detailed output (including bar graphs and hypertext links). More information can be found at www.analog.cx.
- **AWStats** — The Advanced Web Statistics tool (*awstats* package) produces graphical statistics representing Web Server access. AWStats can work with log files in the Apache common log format, as well as log files from Sendmail, FTP, and other network servers. It can report statistics, such as the number of people who have visited, visits made per person, the domain and country of each visitor, and the number of visits made by robots.

## Summary

Web Servers are responsible for storing and delivering the vast amount of content available on the World Wide Web to clients all over the world. Although several Web Server software packages are available for CentOS systems, the most popular is by far the Apache Web Server.

This chapter described how to install, configure, and run an Apache server in CentOS. The httpd daemon process handles requests for Web content (HTTP). Configuration files define what content is made available and how it can be accessed. In particular, the /etc/httpd/conf/httpd.conf file is used to configure the server.

The Apache httpd package also includes facilities for logging error and transfer messages. You can look for the access_log and error_log files in the /etc/httpd/logs directory. The access_log file contains information on content requests that have been serviced by the server. The error_log file lists error conditions that have occurred and times when service has been denied. You can use tools such as Webalizer to simplify the viewing of Apache log data.

# Part IV Networking

# Chapter 21

# Setting Up an LDAP Address Book Server

Sometimes an organization needs a convenient way to gather, store, and distribute information for access by the applications that need it. The Lightweight Directory Access Protocol (LDAP) simplifies the process of creating and using directories of information by network-ready applications.

The intention of LDAP is to simplify the overhead needed to provide directory services described in the X.500 specification. LDAP is a subset of X.500 features. By standardizing the structure of database information, LDAP can get around proprietary storage formats to allow many different applications to share the same data.

> **NOTE** X.500 is a CCITT specification that has become part of the Open Systems Interconnection (OSI) standards that define a layered framework for interconnecting networks and related services. With the dominance of TCP/IP networks (such as the Internet) in the world, OSI never became the predominant network framework that some expected it to be. Despite that, the seven-layer OSI reference model is often used in classrooms to teach networking theory. Likewise, some of these specifications, such as X.500, have been adopted (and sometimes adapted) where standard, cross-platform features are required.

CentOS systems include OpenLDAP software packages to implement LDAP server and client services. To illustrate how to configure and use an LDAP server with OpenLDAP and make it accessible to user applications, this chapter goes through the process of setting up a shared address book to run on a CentOS system. It also describes how to use e-mail clients that can access the LDAP address book.

**IN THIS CHAPTER**

- Understanding LDAP
- Using OpenLDAP
- Configuring an LDAP server
- Creating an LDAP address book
- Using Thunderbird to access the address book

## Understanding LDAP

LDAP lets people create directories of information that can be shared among client applications over a network. It is particularly geared toward applications that are used to look up information that is fairly stable over and over again (in other words, information that’s being looked at more than it’s being changed). That’s why LDAP is popular for uses such as storing information about people, addresses, and other kinds of data that may require high access with relatively few changes.

Because of LDAP’s extraordinarily flexible design, as an LDAP developer or administrator you have a lot of control over:

- How the information in the directories is organized.
- How and by whom information can be accessed.
- The scale, local to global, by which information is distributed. (Information can be replicated to other servers at any scale you choose and synced up automatically.)

As an example, an LDAP address book might resemble the following:

```text
dc=example,dc=com
    ou=members
        cn=Andrew Smith
            homeAddress
            homeTelephone
            workAddress
            workTelephone
        cn=John Wilson
            homeAddress
            homeTelephone
            workAddress
            workTelephone
    ...
```

Despite its flexibility, however, you don’t have to begin designing each directory you create from scratch. LDAP has many predefined structures of information you can rely on to build your LDAP directories.

> **TIP** Microsoft’s Active Directory (AD) is often touted as an “LDAP-based” entity, giving some users high hopes of integrating OpenLDAP and AD. While it is possible to exchange information between AD and OpenLDAP, setting this up requires a lot of patience and skill. Unless you must interoperate with AD, a better path for supporting Windows clients is through the use of OpenLDAP and Samba.

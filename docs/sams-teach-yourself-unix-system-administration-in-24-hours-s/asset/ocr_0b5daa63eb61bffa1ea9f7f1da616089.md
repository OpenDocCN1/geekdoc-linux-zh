Before we finish up this section, let's disable all the services in inetd.conf (use vi and add # before each enabled service). We can double-check the results with the enabled script:

```
# enabled
Services enabled in /etc/inetd.conf are:
#
```

The inetd super-daemon is a great help for the harried sysadmin trying to keep track of what services are enabled, and what binaries the daemons actually use for each service. It's easy to not pay attention and have unnecessary services enabled, which is a definite problem, so you should always double-check the state of the inetd.conf file on your servers. In particular, make sure that the default configuration from the vendor doesn't enable a bunch of unnecessary services. And check again each time you upgrade your OS, just in case things change.

# Managing inetd Security with TCP Wrapper

Although some systems run a stock inetd service and have the program launch daemons directly, this isn't the best security policy in the world. Among other problems, this doesn't enable any sort of control over which remote systems can or cannot access a given service. For example, perhaps your server should allow FTP access from anywhere else in the company, but reject connections from elsewhere on the Internet; or there are competitors who would love to break in through telnet, and you'd like to disable their access.

TCP Wrapper enables just this level of control over access to individual services, and it lets you specify access through allow lists or deny lists.

# Task 19.2: Working with TCP Wrapper

Originally written by Wietse Venema of Eindhoven University of Technology in the Netherlands, TCP Wrapper is actually a rather simple service, but quite helpful nonetheless. It's also installed by default on many flavors of Unix.

+   1. Services monitored with TCP Wrapper are logged in the syslog log file, usually /var/log/messages or /var/log/system.log, depending on the OS. On Mac OS X, for example, an earlier telnet connection and the ftp test from a remote system are logged as

```
# tail -4 /var/log/system.log
Apr 22 21:39:38 ds1-132 telnetd[922]: connect from 63.101.93.250
Apr 22 21:41:17 ds1-132 ftp[d943]: connect from 63.101.93.250
Apr 22 21:41:18 ds1-132 ftp[d943]: connection from 63.101.93.250
Apr 22 21:41:21 ds1-132 ftp[d943]: ANONYMOUS FTP LOGIN REFUSED FROM
->63.101.93.250
```
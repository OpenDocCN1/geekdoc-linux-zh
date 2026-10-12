You should routinely monitor the following log files:

+   • */var/log/messages* contains a wide variety of logging messages from user logins to messages from services started by the TCP wrapper.
+   
+   • */var/log/secure* contains reports from services such as *in.telnetd* and *in.ftpd* that the TCP wrapper starts.
+   
+   • */var/log/mailog* contains reports from *sendmail*.
+   
+   • */var/log/xferlog* contains a log of all FTP file transfers.

Unfortunately, there is no easy-to-use tool for viewing these log files. The best approach is to browse them routinely using a text file viewer such as *less* or *more* to prevent accidentally overwriting one of the log files. Using *less* or *more*, you can search for a date of interest and begin browsing from that point in the file.

Because many potential intruders use port-scanning tools that attempt to establish TCP/IP connections to well-known ports on your system, you should look for messages that indicate attempted connections from unknown hosts (indicated by names or IP addresses). For such attempted network accesses, you should browse through the */var/log/secure* file. For example, here's what a line in the */var/log/secure* file shows when connecting to a sample Linux system from one of the PCs on a LAN:

```
Aug 16 20:18:19 lnbp200 xinetd[511]: START: ftp pid=23824 from=192.168.1.40
```

Notice the text *pid=23824*, which appears next to the word *ftp*. That's the process ID of the FTP server program started by *xinetd*. You can use this number to look at corresponding messages in the */var/log/messages* file to see whether this attempt did or did not succeed. Here is a sample of how you could check this:

```
grep "*[23824]*" messages
Aug 16 20:30:01 lnbp200 ftpd[23824]: FTP LOGIN FROM lnbp400 [192.168.1.40], naba
Aug 16 20:30:22 ftpd[23824]: FTP session closed
```

The resulting output tells you that the user *naba* successfully logged in and sometime later closed the FTP session.

To identify the host name associated with an address, use the command *dig -x ipaddress*, where *ipaddress* is the IP address in which you are interested.

In a similar manner, you should analyze any suspicious messages you find in these log files. You may be surprised by the number of attempts curious outsiders make to gain access to your system.

# Security news and updates

To keep up with the latest security alerts, you may want to visit one or more of the following sites on a daily basis:

+   • CERT Coordination Center at *http://www.cert.org/*
+   
+   • Computer Incident Advisory Capability (CIAC) at *http://www.ciac.org/*
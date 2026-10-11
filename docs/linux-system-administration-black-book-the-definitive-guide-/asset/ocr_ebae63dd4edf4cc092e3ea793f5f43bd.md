# Table 18.2 Print system types available in /etc/smb.conf.

| Type | Operating System |
| --- | --- |
| AIX | A Unix flavor created and maintained by IBM |
| BSD | A Unix flavor created by Berkeley Software Distribution at the University of California at Berkeley and now maintained by Berkeley Software Design |
| HPUX | A Unix flavor created and maintained by Hewlett-Packard |
| LPRNG | A print spooling system based on that used by BSD; this is the collection of print tools used under many Linux distributions, including Red Hat |
| PLP | A print spooling system that also is used under some Linux distributions, such as SuSE |
| QNX | A Unix-flavor realtime operating system |
| SOFTQ | Another real-time Unix operating system |
| SYSV | A Unix flavor created and maintained by AT&T |

As with most network services, several logging options are available with Samba. These statements are important because they enable you to keep data regarding connections, attempted connections, and more. The more data you have available, the better chance you have of catching potential intruders.

The log file statement sets the name and path of the file that Samba logs information to. Having %m at the end of the file name means that there will be a series of log files in the location specified by the path in this statement, each with the name log.NetBIOS. Other variables used in /etc/smb.conf are listed in Table 18.3.

After setting the log file’s name and location, you reach this line:

```
max log size = 50
```

The max log size directive sets how large Samba should let its log files get. The associated value is in kilobytes, and using a 0 means the log file size is unlimited—a bad idea, unless you enjoy having your file system overrun by log files. When a file reaches the listed size, Samba renames the existing file with an .old extension and starts a new file using the original name. You can then have shell scripts—discussed in Chapter 20—back up and compress these files so that you can keep them for analysis, if you need them, without filling up the file system.

After you finish with the log information, it is time to move on to security:

```
security = user
```

The security statement determines how clients authenticate themselves with the server. There are four different security modes available in Samba 2, which is what you are using if you have Red Hat 6.2 or later. These modes are:
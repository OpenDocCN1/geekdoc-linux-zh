# xineted Configuration

```
-r-xr-xr-x 3 root 42897 Apr 15 10:02 libnss_files-2.2.5.so
lrw-xr-wwx 1 root 21 May 14 09:46 libnss_files.so-2 -> |\libnss_files-2.2.5.so
-r-xr-xr-x 1 root 260 May 14 09:48 libmd5
lrw-xr-wwx 1 root 19 May 10 11:36 libtermcap.so.2-0 -> |\libtermcap.so.2-0.8
-r-xr-xr-x 2 root 11832 Jul 9 2001 libtermcap.so.2.0.8
```

```
/var/ftp:
total 8
d-xr-xr-x 2 root ftp 4096 Aug 22 2001
d-xr-xr-x 6 root root 4096 May 10 11:36 .. .
```

> A good reference for locking down FTP can be found at http://www.redhat.com/support/resources/tips/FTP-Setup-Tips/FTP-Setup.html.

# xineted Configuration

xineted (pronounced "zy-net-d") is Red Hat's extended Internet services daemon that handles incoming connections for network services. xineted is the preferred replacement for a similar tool (used with other Linux distributions and older Red Hat releases) called inetd. However, in addition to several other improvements over inetd, xineted allows you to apply individual access policies to different network connection requests, as as FTP.

This daemon controls a number of services on your system according to settings in configuration files under the /etc/xinetd. directory. This section will show you how to edit the appropriate files to enable the use of wu-ftp and vsftpd FTP servers.

# Configuring xineted in the wu-ftp Server

When installing wu-ftp, the RPM package contains an xineted configuration file, /etc/xinetd/wu-ftpd, as seen in Listing 18.3. You need to edit the file because default settings disable incoming FTP requests.

> Don't be confused by the first line of the wu-ftp file's text. Even though it reads default: on, FTP service is off unless you specifically configure its use. The line is a comment because it begins with a pound sign (#) and is ignored by xinetd. Whether FTP service is on is determined by the text line disable = yes.
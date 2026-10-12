# QUICK AND DIRTY FTP SERVICE

Conscientious Linux administrators take the time to carefully install, set up, and configure a production FTP server before offering public service or opening up for business on the Internet. However, you can set up a server very quickly on a secure LAN by following a few simple steps:

+   1.  Ensure that the FTP server RPM package is installed, networking is enabled, and firewall rules on the server allow FTP access. See Chapter 18, “Network Connectivity,” to see how to use Red Hat’s system-config-securitylevel client for firewalling.

+   2.  If anonymous access to server files is desired, populate the /var/ftp/pub directory. Do this by mounting or copying your content, such as directories and files under this directory.

+   3.  Edit and then save the appropriate configuration file (such as vsftpd.conf for vsftpd) to enable access.

+   4.  If you are using wu-ftpd, you must start or restart xinetd like so: /etc/rc.d/init.d/ xinetd restart. If you are using vsftpd, you must start or restart the server like so: service vsftpd start.

# xinetd Configuration for wu-ftpd

xinetd (pronounced “zy-net-d”) is the extended Internet services daemon, and handles incoming connections for network services. xinetd is the preferred replacement for a similar tool (used with other Linux distributions and older Red Hat releases) called inetd. However, in addition to several other improvements over inetd, xinetd allows you to apply individual access policies to different network connection requests, such as FTP.

This daemon controls a number of services on your system according to settings in configuration files under the /etc/xinetd.d directory. This section shows you how to edit the appropriate files to enable the use of the wu-ftpd FTP server.

# Configuring xinetd for the wu-ftpd Server

When installing wu-ftpd using RPM, the RPM package might contain a xinetd configuration file, /etc/xinetd.d/wu-ftpd, as seen in Listing 24.3. You need to edit the file because its default settings disable incoming FTP requests.

# NOTE

> Do not be confused by the first line of the wu-ftpd file’s text. Even though the line reads default: on, FTP service is off unless you specifically configure its use. The line is a comment because it begins with a pound sign (#) and is ignored by xinetd. Whether FTP service is on is determined by the text line disable = yes.
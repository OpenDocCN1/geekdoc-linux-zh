FTP 513

shutdown /etc/shutmsg

passwd-check rfc822 warn

Check the man pages ftpacces and fthosts for information on the
format of the configuration directives.

# # Administration

By default, the FTP service is run as an inetd service. Thus, it is not necessary
to start, restart, or stop the service.
The FTP service places log entries in the system log, /var/log/messages.
If the FTP service is not operating properly, check the contents of the system
log for log entries that point to the problem.
A common requirement is for a set of directories to be accessible via anon-\ym FTP, HTTP, and NFS. The FTP server does not follow symbolic links,
so directories must be subdirectories of the directory designated as the
home directory of the ftp user, generally /home/ftp directory. To provide
access via HTTP, establish symbolic links pointing to the directories. To pro-
vide via NFS, simply export the directories.

# # Further Information

You can find further information on FTP in the man page for ftp and ftpd,
an pages for ftpaccess and fthosts, and on the Web at www.wu-ftpd.org.
To try your hand at installing and configuring FTP, complete Exercise 21.3.

| EXERCISE 21.3 |

Installing FTP
FTP is a popular service, so you should be certain you're familiar with
its installation, configuration, and operation. To gain first-hand experience,

+   1. Install the wu-ftpd and anonftpd packages.
2. Verify that you can log in and perform transfers using a defined
user account.

Copyright ©2000 SYBEX, Inc., Alameda, CA www.sybex.com
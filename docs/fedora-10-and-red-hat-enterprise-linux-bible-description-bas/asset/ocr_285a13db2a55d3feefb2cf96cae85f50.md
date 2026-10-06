# Appendix B: Running Network Services 1019

you have a valid name (IP address) for your Web server. To define a server name, add a ServerName to the http.conf file and restart the server.

Users who can access your system from the network will be able to view the contents of the /var/www/html directory, by default. Replace the index.html file and add your own content. If the httpd-manual package is installed, /var/www/manual contains the apache manual.

> CROSS-REFERENCE: See Chapter 21 for information on configuring an Apache server.

# File servers

File servers in Fedora and RHEL can be provided by FTP servers, Samba (Windows) servers, Network File System (NFS), and NetWare servers. The following sections describe each of these.

# FTP servers

The Secure FTP daemon (vsftpd) package was designed from scratch to be very scalable and fast. It is geared towards FTP sites that require support for lots of simultaneous users. Configure vsftpd by editing the /etc/vsftpd/vsftpd.conf and /etc/vsftpd/user_list files. The vsftpd package shares the /var/ftp directory structure and listens on port 21 for service requests.

To turn on FTP service, type the following (as root user):

```
# service vsftpd start
# chkconfig vsftpd on
```

Another FTP server is the Trivial FTP server (tftpd). Tftpd is often used as a boot server for projects such as the Linux Terminal server project.

> CROSS-REFERENCE: See Chapter 20 for information on how to configure the vsftpd server.

> NOTE: An FTP server with Kerberos 5 support is also included with Fedora and RHEL. The krb5-workstation package contains the ftppd daemon that includes Kerberos 5 support. The wu-ftp FTP server is no longer in the Fedora or RHEL distributions.

# Samba server

The Samba server supports the Server Message Block (SMB) and CIFS file- and printer-sharing protocols. SMB and CIFS are often used to share resources on local networks consisting of computers running Microsoft Windows. You would not typically use SMB/CIFS files and printers over a public network, such as the Internet.
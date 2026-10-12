+   * **Daemon:** What daemon process is running to provide the service? 
+   * **Configuration files:** What configuration files can you modify to tailor the service to your specific needs?

The descriptions following the table provide additional information about the service. That information includes whether or not the service is started by default and where you can find more information about the service.

> **NOTE:** When the *xinetd* daemon is noted as the start-up script, the daemon process to which the service is handed off is also noted.

The following sections provide some additional information about the services described in Table C-1.

# Web server

In most cases, you use the apache software package to create a Web server in Red Hat Linux. If apache is installed, you must turn on the service to use it (as root user, type `chkconfig httpd on`). Start-up will fail unless you have a valid name (and IP address) for your Web server. To define a server name, add a `ServerName` entry to the `httpd.conf` file and restart the service.

Users who can access your system from the network will be able to view the contents of the `/var/www/html` directory. Replace the `index.html` file and add your own content. If the httpd-manual package is installed, `/var/www/manual` contains the apache manual.

> **CROSS-REFERENCE:** See Chapter 21 for information on configuring an Apache Web server.

An alternative to apache is the TUX HTTP server. TUX is a high-performance Web server. The entire protocol stack for TUX runs in the Linux kernel. Configure TUX in the `/etc/sysconfig/tux` file. The TUX service is off by default. To turn it on, type `chkconfig tux on` and it will start the next time you start your computer. It will offer the same content that apache does (from the `/var/www/html` directory).

# File servers

File services in Red Hat Linux can be provided using FTP servers, Samba (Windows) servers, Network File System (NFS) servers, and NetWare servers. The following sections describe each of these.

# FTP servers

The Very Secure FTP daemon (vsftpd) package was designed from scratch to be very scalable and fast. It is geared toward FTP sites that require support for lots of simultaneous users. Configure vsftpd by editing the `/etc/vsftpd.conf` and `/etc/vsftpd.user_list`
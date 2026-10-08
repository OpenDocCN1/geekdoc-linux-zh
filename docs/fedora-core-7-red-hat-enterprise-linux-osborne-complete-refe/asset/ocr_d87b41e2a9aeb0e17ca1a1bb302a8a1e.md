# ## Available Servers

Several FTP servers are available for use on Fedora and Red Hat systems (see Table 22-1). Three Fedora-compliant servers included with Fedora are **vsftpd**, **pureftpd**, and **proftpd**. The Very Secure FTP Server, **vsftpd**, provides a simple and very secure FTP server. The Pure FTPD, **pureftpd**, server is a lightweight, fast, and secure FTP server, based upon Troll-FTPD. Documentation and the latest sources are available from **www.pureftpd.org**.

ProFTPD, **proftpd**, is a popular FTP daemon based on an Apache Web server design. It features simplified configuration and support for virtual FTP hosts. The compressed archive of the most up-to-date version, along with documentation, is available at the ProFTPD Web site at **www.proftpd.org**. Another FTP daemon, NcFTpd, is a commercial product produced by the same programmers who did the NcFTP FTP client. NcFTPd is free for academic use and features a reduced fee for small networks. Check **www.ncftpd.org** for more information.

Several security-based FTP servers are also available, including SSLFTP and SSH **sftpd**, along with **gsftpd**. SSLFTP uses SSL (Secure Sockets Layer) to encrypt and authenticate transmissions, as well as MD5 digests to check the integrity of transmitted files. SSH **sftpd** is an FTP server that is now part of the Open SSH package, using SSH encryption and authentication to establish secure FTP connections. The **gsftpd** server is part of the Kerberos 5 package and provides Kerberos-level security for FTP operations.

# ## Fedora and Red Hat FTP Server Directories

The **vsftpd** server package is part of Fedora. If you choose to install an FTP server, the **vsftpd** server package is installed along with anonymous FTP support. An **ftp** directory is created along with several subdirectories where you can place files for FTP access. The directories are configured to control access by remote users, restricting use to only the **ftp** directories and any subdirectories. The **ftp** directory is placed in the */var* directory, */var/ftp*. Place the files you want to allow access to in the */var/ftp/pub* directory.

You can also create subdirectories and place files there. Once you are connected to a network, a remote user can connect to your system and download files you placed in */var/ftp/pub* or any of its subdirectories. The **vsftpd** FTP package implements a default configuration for those directories and their files. You can change these if you want. If you

| FTP Servers | Site |
|---|---|
| Very Secure FTP Server (vsftpd) | **vsftpd.beasts.org** (Fedora) |
| ProFTPD | **www.proftpd.org** |
| PureFTP | **www.pureftpd.org** |
| NcFTPd | **www.ncftpd.org** |
| SSH sftp-server | **www.openssh.org** |
| Washington University Web server (WU-FTPD) | **www.wu-ftpd.org** |
| Tux | Web server with FTP capabilities |
| gsftpd | Kerberos FTP server |

# **TABLE 22-1** FTP Servers
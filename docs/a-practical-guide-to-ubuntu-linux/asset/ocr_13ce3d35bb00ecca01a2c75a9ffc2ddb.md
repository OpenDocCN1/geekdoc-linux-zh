# INTRODUCTION TO FTP

This chapter starts with an introduction to FTP which discusses security, describes types of FTP connections, and presents a list of FTP clients. The first JumpStart section covers ftp commands and includes a tutorial on using the ftp client. Next is a section that presents more details of ftp. The final section describes how to set up a vsftpd server.

First implemented under 4.2BSD, FTP has played an essential role in the propagation of Linux; this protocol is frequently used to distribute free software. The term FTP site refers to an FTP server that is connected to a network, usually the Internet. FTP sites can be public, allowing anonymous users to log in and download software and documentation. In contrast, FTP sites require you to log in with a username and password. Some sites allow you to upload programs.

History

Most FTP clients are similar, the servers differ quite a bit. This chapter describes ftp with references to sftp, a secure FTP connection. It also covers the FTP server available under Ubuntu, which is named vsftpd (very secure FTP daemon).

ftp and vsftpd

The ftp utility is a user interface to FTP, the standard protocol used to transfer files between systems that communicate over a network.

ftp utility

# SECURITY

FTP is not a secure protocol: All usernames and passwords are exchanged in setting up an FTP connection is not encrypted, and the connection is subject to hijacking. Given these facts, FTP is best used for downloading public files. In most cases, the OpenSSH client, ssh (page 670), scp (page 672), and sftp (page 674), offer secure alternatives to FTP.

Use FTP only to download public information

FTP is not secure. The vsftpd utility provides better security for all FTP functions other than allowing anonymous users to download information. Because vsftpd uses an encrypted connection, user passwords and data cannot be sniffed when you use this utility. You can replace instances of ftp in this chapter with sftp because vsftpd uses the same commands as ftp. See page 674 for more information on sftp.

security

The vsftpd server does not make usernames, passwords, data, and connections more secure. However, it is secure in that a malicious user finds it difficult to compromise the directly system running it, if vsftpd is poorly implemented. One feature that makes vsftpd more secure than ftp is that it does not run with root privileges. See also “Security” on page 699.

# FTP CONNECTIONS

FTP uses two connections: one for control (you establish this connection when you log in an FTP server) and one for data transfer (FTP sets up this connection when
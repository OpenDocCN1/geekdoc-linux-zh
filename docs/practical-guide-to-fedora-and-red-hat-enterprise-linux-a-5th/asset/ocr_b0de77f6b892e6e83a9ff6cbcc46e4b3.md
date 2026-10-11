# # INTRODUCTION

First implemented under 4.2BSD, FTP has played an essential role in the propaga- tion of Linux; this protocol/program is frequently used to distribute free software. The term FTP site refers to an FTP server that is connected to a network, usually the Internet. FTP sites can be public, allowing anonymous users to log in and download software and documentation. In contrast, private FTP sites require you to log in with a username and password. Some sites allow you to upload programs.

Although most FTP clients are similar, the servers differ quite a bit. This chapter describes the ftp client with references to sftp, a secure FTP client. It also covers the FTP server that Red Hat uses internally and offers as part of its distribution, vsftpd (very secure FTP).

FTP is not a secure protocol. All usernames and passwords exchanged in setting up an FTP connection are sent in cleartext, data exchanged over an FTP connection is not encrypted, and the connection is subject to hijacking. FTP is best used for down- loading public files. In most cases, the OpenSSH clients, ssh (page 627), scp (page 630), and sftp (page 631), offer secure alternatives to FTP.

# ## Use FTP only to download public information

> FTP is not secure. You can use scp for almost all FTP functions other than allowing anonymous users to download information. Because scp uses an encrypted connection, user passwords and data cannot be sniffed. See page 630 for more information on scp.

The vsftpd server does not make usernames, passwords, data, and connections more secure. The vsftpd server is secure in that a malicious user finds it more diffi- cult to compromise directly the system running it, even if vsftpd is poorly imple- mented. One feature that makes vsftpd more secure than ftpd is that it does not run with root privileges. See also “Security” on page 655.

The ftp utility is a user interface to File Transfer Protocol (FTP), the standard proto- col used to transfer files between systems that can communicate over a network.

Part of the OpenSSH suite, sftp is a secure alternative to ftp. See page 631 for more information.

FTP uses two connections: one for control (you establish this connection when you log in an on FTP server) and one for data transfer (FTP sets up this connection when you ask it to transfer a file). An FTP server listens for incoming connections on port 21 by default and handles user authentication and file exchange.

A client can ask an FTP server to establish either a PASV (passive—the default) or a PORT (active) connection for data transfer. Some servers are limited to only one type of connection. The difference between a passive and an active FTP connection lies in whether the client or server initiates the data connection. In passive mode, the client initiates the connection to the server (on port 20 by default); in active mode, the server initiates the connection (there is no default port; see “Connection Param- eters” on page 664 for the parameters that determine which ports are used). Neither is inherently more secure than the other. Passive connections are more common
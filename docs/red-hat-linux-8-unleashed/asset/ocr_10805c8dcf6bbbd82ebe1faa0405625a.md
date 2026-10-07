# Using FTP

FTP is a client/server used to connect to the server. Nearly all FTP clients allow file transfers and display remote directories. If enabled, clients can also allow users to create or modify remote directories.

Note however, using FTP can pose a security risk: Usernames and passwords are transmitted in clear text across a LAN or the Internet. For this reason, many sites enable anonymous FTP login and file retrieval. The following sections discuss the different types of traditional and newer interfaces to FTP and their usage.

# Using sftp for Secure FTP User Transactions

Use the Secure File Transfer sftp command, a component of the OpenSSH distribution, to bypass the use of an FTP server and enable secure network file transfer. The sftp client uses the sftp-server which is not set up or configured as an FTP server, but is part of the ssh daemon. Sftp provides the benefit of username and password encryption when logging in, and your username and password will not be transmitted in clear text across a network. Although sftp not have the directory listing features of ftp (with wildcard expressions), it has 52 built-in commands with similar matching capabilities.

You can use sftp to access a server of OpenSSH (which consists of openssh-askpass-3.4p1-2, openssh-server-3.4p1-2, openssh-clients-3.4p1-2 and openssh-3.4p1-2 RPM packages) is installed and the ssh daemon is running. Secure access is by default, but can be controlled by editing the subsystem-sftp entry in /etc/ssh/sshd_config and restarting sshd (see Chapter 7, “Managing Services,” to see how to start, stop, or restart services). A companion command sc can also be used to transfer files, but requires prior knowledge of the remote computer's file system and a specific pathname on the command line.

Data rates will take a hit because of the overhead of encryption, but by use of a secure session might be more important, especially if you're transferring files over an insecure network, or as a wireless LAN.

# The FTP Client Interface

In Red Hat Linux, you can use either a graphical or a text-based FTP interface. No matter which type you choose, you can improve your understanding and use of FTP if you learn how to use the FTP client on the text level.

Using the text-based interface helps understand what each action in a graphical interface does. This understanding is particularly handy when, for example, the graphic client doesn't automatically detect the file type that is being transferred. In this situation, a binary file is transferred as an ASCII file and conversely, an ASCII file is transferred as a binary with the “M control character at the end of each line. This error typically occurs when transferring a file from Microsoft Windows to Linux.
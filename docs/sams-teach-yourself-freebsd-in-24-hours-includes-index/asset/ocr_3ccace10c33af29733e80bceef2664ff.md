> You can replace FreeBSD's default FTP server with any of a number of other choices—some of the more popular being WU-FTPD and ProFTPD. These are available in the ports (/usr/ports/ftp) or the packages (under ftp).

The file layout of the FTP server, in the default configuration, is integrated with the system in the same way that most other core services are. Several configuration files are in /etc—some of which do double duty as systemwide resource files used by other services. Individual users' home directories are considered part of the FTP server layout because each authenticated user connects directly into his home directory.

Because anonymous FTP requires a bit more configuration and maintenance than regular authenticated FTP, though, we must examine the difference between them a little more in depth.

# Authenticated and Anonymous FTP

When a user who has an account on the server logs in via FTP with his username and password, the server provides access to the user's home directory and all its files. The user can enter an ls command to verify this. Each regular user thus connects to a different point on the FTP server when logging in as a user: his home directory. However, anonymous FTP provides a way for a user without an account to connect. An anonymous user opens the connection, enters anonymous or ftp as his username, and any text string (conventionally the user's email address, though this usually isn't enforced or authenticated in any way) for the password. The user is then given access to a public FTP area: /var/ftp, the home directory of the ftp user (which is also created when anonymous FTP is enabled), as shown in Figure 24.1.

FIGURE 24.1
*Authenticated and anonymous FTP users.*

![](bbox=[0.38, 0.85, 0.66, 0.97])

A fundamental difference exists between regular account users and anonymous FTP users, though. Anonymous FTP is in a chroot jail by default (chroot means “change
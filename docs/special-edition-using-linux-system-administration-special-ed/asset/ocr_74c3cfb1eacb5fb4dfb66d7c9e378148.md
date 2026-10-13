+   13. If this line is missing from `inetd.conf`, add the line, save the file, and restart `inetd` by sending it a SIGHUP signal as outlined in Chapter 8, “Linux Process Management and Daemons.”

When installed using these steps, you will have a standard password-protected FTP server.

# Testing Your New WU-FTP Installation

After you have installed WU-FTP, you should double-check that it is running properly. To do this, use the FTP client included with your Linux distribution to connect to the new FTP server and log in as an existing user to whom you have allowed access to your FTP server in `/etc/ftppaccess`:

```
```text
# ftp localhost
Connected to localhost.
220 linux.juxta.com FTP server (Version wu-2.6.0 (1) \
    Mon Apr 19 09:21:53 EDT 1999) ready.
Name (localhost:root):
331 Password required for username.
Password:
230 User username logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> pwd
257 "/home/username" is the current directory.
ftp> bye
```
```

If you can successfully connect to the server, log in and display the current directory as shown in this example. You have successfully installed WU-FTPd.

# Anonymous FTP Setup

When you have a functioning FTP server either installed with your distribution or compiled from the source code, you can configure it to accept anonymous access using the following steps:

> **Note:** Many Linux distributions that install WU-FTPd as a binary package will pre-configure the software to accept anonymous connections. You can check this by connecting to your FTP server as an anonymous user.

+   1. Create a user to be used for anonymous access. Usually, this user is called `ftp`. The account you create should have a unique home directory. On most Linux systems this home directory will be `/home/ftp/`. You can create this user and home directory using the procedures described in Chapter 3, “User and Group Administration.”
# 470 Linux Administration: A Beginner's Guide

+   3. You must enter the password for the user yangyang prompted:
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

+   4. Use the pwd command to display your present working directory on the FTP server. You will notice that the directory shown is the home directory for the user yangyang.
ftp> pwd
257 "/home/yang"

+   5. Using the cd command, try to change to a directory outside of yangyang's FTP home directory; for example, try to change the directory to the /boot directory of the local file system:
ftp> cd /boot
250 Directory successfully changed.

+   6. Log out of the FTP server using the bye command:
ftp> bye
221 Goodbye.

As demonstrated by these FTP sessions, the default vsftpd configuration on our sample Fedora system allows these FTP sessions:

+   - Anonymous FTP access Any user from anywhere can log into the server using the username ftp (or anonymous), with anything at all for a password. This is not the case on Debian-like distros like Ubuntu.
- Local logins All valid users on the local system with entries in the database (the /etc/passwd file) are allowed to log into the FTP server using their normal usernames and passwords. This is true with SELinux in permissive mode. On our Ubuntu server, this behavior is disabled out of the box.

# Customizing the FTP Server

The default out-of-the-box behavior of vsftpd is probably not what you want for your production FTP server. So in this section we will walk through the process of customizing some of the FTP server's options to suit certain scenarios.
server’s system (the `/var/ftp` directory, by default, on Red Hat Linux systems). There were probably restrictions on what I could change, delete, or create on the server as an anonymous user as well.

One of the great advantages of anonymous FTP is that it can easily be automated. Instead of using the `ftp` command, users can simply type the FTP address of the server into a Web browser. Users don’t even need to know that they are being logged in as an anonymous user when they visit the FTP site. The list of files and directories requested simply appears.

> **TIP:** Assuming you have installed the `anontftp` software package and started the FTP service, anonymous users are given access to your FTP server by default. This assumes that your firewall is not blocking access to the service and that `disable = yes` was changed to `disable = no` in the file `/etc/xinetd.d/wu-ftpd`. To prevent anonymous users from accessing your FTP server, add the following line to your `/etc/ftpaccess` file:
> 
> `defaultserver private`

# Real users

The users who have valid login accounts to your computer can also access the computer via FTP. These users can have any user name that the administrator defines. To use FTP, they can simply type their user names and passwords at the FTP prompts. At that point, they will be logged in to the FTP server.

> **CROSS-REFERENCE:** See Chapter 11 for information on setting up regular real user accounts.

Instead of having `/var/ftp` as their root directory, however, real users have their regular home directory (such as `/home/user`, where `user` is the user name) as their root directory and current directory when they log in. Like the anonymous user, the real user has special restrictions with regard to the file system. By default, real users cannot access any files outside of their home directory and related subdirectories.

> **NOTE:** If you used WU-FTPD in a Red Hat Linux system prior to version 7.3, you may remember that real users’ access was not restricted to their home directory. If your users complain, you can consider reconfiguring the `ftpaccess` file.

No special configuration needs to be done in the `/etc/ftpaccess` file to allow a user with a real account to connect to the server through FTP. However, if you want to provide one or more real users with the same access to the file system that they would have if they logged in directly, you could redefine that user or group as real by setting a `realuser` or `realgroup` value for the user or group, respectively. (For example, add a line that reads `realuser joe` to give the user named `joe` access to files outside of his home directory.)

To prevent any real user from using the FTP service, you can simply add the person’s user name to the `/etc/ftppers` list. By default, these users are excluded because they are on this list: `root`, `bin`, `daemon`, `adm`, `lp`, `sync`, `shutdown`, `halt`, `mail`, `news`, `uucp`, `operator`, `games`.
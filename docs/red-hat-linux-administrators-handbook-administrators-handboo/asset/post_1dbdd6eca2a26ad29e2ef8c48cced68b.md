
## /etc/ftpconversions

The ftpconversions file stores the FTP server's conversion database. The default configuration for this file is sufficient for almost all installations. If you need more information, see the man page for ftpconversions.

## /etc/ftpgroups

The file /etc/ftpgroups is important only if you allow the nonstandard SITE commands. The Red Hat-shipped wu-ftpd package comes with the SITE commands disabled, to enhance security, because SITE commands have been known to create security holes in earlier versions of the server. For the sake of completeness, the purpose of this file is described, but its use is strongly discouraged.

When a not-so-security-savvy FTP administrator enables the SITE commands, she needs to set up the /etc/ftpgroups file as follows:

```
groupname:encrypted password:realgroup
```

Typically, the SITE GROUP and SITE GPASS commands are used to allow an already-logged-in FTP user to upgrade her group privileges. The /etc/ftpgroups file provides the necessary mapping for a user of groupname to be upgraded to the realgroup when a valid password is entered using the SITE GPASS command. Also note that the realgroup must be a group in the /etc/group file.

## /etc/ftphosts

The file /etc/ftphosts is used to control FTP access to specific accounts from various hosts. To allow a user to log in from one or more hosts, use a line such as the following:

```
allow username addrglob [addrglob . . .]
```

This allows the specified user to log in from the specified hosts. For example,

```
allow joegunchy *.nitec.com
```

allows the user joegunchy to log in from any machine in the nitec.com domain. To deny a user the ability to log in to the server from one or more hosts, use the following line:

```
deny username addrglob [addrglob . . .]
```

For example, to prevent joegunchy from logging in to the server from the 206.171.50.0 network, use the following line:

```
deny joegunchy 206.171.50.*
```

## /etc/ftpusers

The file /etc/ftpusers specifies the list of users who are not allowed to access the FTP server. The default /etc/ftpusers file contains the following users:

|  |  |
|---|---|
| root | halt |
| bin | mail |
| daemon | news |
| adm | uucp |
| lp | operator |
| sync | games |
| shutdown | nobody |

These accounts are not allowed to log in, because they are not real user accounts. If you need to stop a real user from being able to FTP to the server, put the username in this file.

At this point you have learned about all the configuration files necessary to run the FTP server. Now I will discuss some common FTP server configuration issues in the following sections.

![](img/c2419364ebb911c809b6a79991707c27_262_0.png)

> **Tip**
> Because a lot of configuration is needed for proper FTP service, having a way to verify your configuration files periodically is useful. A utility called ftpck, which you can download from ftp://ftp.landfield.com/wu-ftpd/ftpck/, provides this type of periodic verification.

## Creating an anonymous FTP site

Having an anonymous FTP site can be a mixed blessing. It can be a great medium for distributing files that need to be widely distributed. In fact, all the free software packages (including the Red Hat Linux distribution) that you can download from the Internet are stored in many anonymous FTP sites all around the world. Just think what a nightmare it would be if you needed accounts on each of the FTP servers on the Internet to get access to free software. It simply isn't practical. This problem has been solved with anonymous FTP service. However, anonymous FTP service is also a common gateway for hackers to get into a system. So, think twice before you decide to create an anonymous FTP server.

Fortunately, Red Hat makes creating an anonymous FTP server very easy. You simply need the anonftp RPM package. First, query your RPM database to find out whether you have already installed the anonftp package:

```
rpm -qa | grep anonftp
```

This displays the package name, such as anonftp-2.8-1, if you have already installed the anonftp package as part of your Red Hat Linux installation. If you haven't, however, the preceding command won't produce any output. In such a case, get the latest anonftp package from your Red Hat CD-ROM and run the following:

```
rpm -ivh anonftp-2.8-1.i386.rpm
```

If you want to install the latest version from a Red Hat mirror site, run the following command:

```
rpm -ivh ftp://ftp.cdrom.com/pub/linux/redhat/redhat-6.0/i386/RedHat/RPMS/anonftp-2.8-1.i386.rpm
```

Your anonftp package name will vary with your system architecture and anonftp version. Also, the anonftp package won't install if you don't already have an FTP server, such as wu-ftpd.

After you install the anonftp package, you have an anonymous FTP server ready to run.

## Tip

You must have the user account called ftp, without any password, in the /etc/passwd file before you can use anonymous FTP service. The FTP user account line in your /etc/passwd should look similar to this:

```
ftp:*:14:50:FTP User:/home/ftp:/bin/true
```

If you want to know what the package has installed, run the following:

```
rpm -qlp anonftp-2.8-1.i386.rpm
```

Notice that it has installed all the files under the ~ftp directory (the home directory of the ftp account—see the /etc/passwd file). These files are described next in detail.

Change the directory to ~ftp and enter ls -l. You will see the following directories:

```
[kabir@picaso ~ftp]$ ls -l
total 4
d--x--x--x 2 root root 1024 Nov 5 19:29 bin
d--x--x--x 2 root root 1024 Nov 5 19:29 etc
drwxr-xr-x 2 root root 1024 Nov 5 19:29 lib
dr-xr-sr-x 2 root ftp 1024 Sep 10 17:21 pub
```

Change the directory to the bin subdirectory and run ls -l, as before; you will see something like the following:

```
[kabir@picaso ~ftp/bin]$ ls -l
total 313
---x--x--x 1 root root 15236 Nov 5 20:02 compress
---x--x--x 1 root root 46356 Nov 5 20:02 cpio
---x--x--x 1 root root 45436 Nov 5 20:02 gzip
---x--x--x 1 root root 29980 Nov 5 20:02 ls
---x--x--x 1 root root 62660 Nov 5 20:02 sh
---x--x--x 1 root root 110668 Nov 5 20:02 tar
lrwxrwxrwx 1 root root 4 Nov 5 20:02 zcat -> gzip
```

These are the utilities needed to provide a reasonable anonymous FTP service. The ls utility is used to provide the directory listings, and the compression utilities are used to provide on the fly compression/decompression facilities. These files are provided because the server needs to perform a chroot to the ~ftp directory when someone accesses the anonymous FTP server. The chroot program allows the server to treat the ~ftp directory as the root directory of the system. In other words, when an anonymous FTP user logs in to the server, the server does a chroot to ~ftp and thus hides the real file system, showing only what is under the ~ftp directory. This is why you need a copy of the etc, bin, and lib directories with an absolutely minimal number of files. The lib directory contains the system library files that are needed for the programs in the bin directory. The ~ftp/pub directory is where you should keep the publicly distributable files.

If you need an incoming or dropbox directory to which anonymous users can upload files, do the following:

- 1. Create a subdirectory in the ~ftp directory that will be used for uploads. This directory typically is called "incoming," so that name is used here.
- 2. Add the following line in your /etc/ftpaccess file:
  ```
  upload /home/ftp /incoming yes root ftp 0600 nodirs
  ```
- 3. Change /home/ftp to the appropriate directory. For example, if your ~ftp is really /data/ftp, then change /home/ftp to /data/ftp in the preceding line. Also, if you want to allow anonymous users to be able to create subdirectories under ~ftp/incoming, remove the nodirs option in the preceding line.
- 4. Run the following commands:
  ```
  chown -R root.ftp ~ftp/incoming
  chmod -R 1733 ~ftp/incoming
  ```
  The chown command sets root and ftp as the owner for the incoming directory. The chmod command changes the incoming directory permissions so that root has read, write, and execute (rwx) permissions and the group and the world have write and execute (wx) permissions. It also sets the sticky bit for the directory and all of its files, which protects the files from being deleted by regular users. Normally, when a directory has write and execute permissions set for everyone, any user of that system can delete a file in that directory. The sticky bit stops that by allowing only the creator of the file to delete the file. Because the FTP server writes the file with root as the owner, no one but root is allowed to delete the uploaded files.
- 5. Make sure that you have the anonymous user type listed in at least one of the class definitions in your /etc/ftpaccess file. By default real, guest, and anonymous are all included in the default class, so you don't need to do anything unless you have altered the default class definitions.

After you complete these steps, FTP to the server as an anonymous user and make sure you can upload files only into the specified directory.

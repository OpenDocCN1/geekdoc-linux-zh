
## CHAPTER 17 File Transfer Protocol (FTP) 469

- 1. Enter anything at all prompted for the password:

Password: <type-absolutely-anything-you-want-for-the-password>
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

- 2. Use the ls (or dir) FTP command to perform a listing of the files in the current directory on the FTP server:

```
ftp>
ls
227 Entering Passive Mode (127,0,0,1,63,215)
150 Comes the directory listing.
drxr-x- 2 0 0 4096 Aug 29 06:18 pub
226 Directory sent.
```

- 3. Use the pwd command to display our working directory on the FTP server:

```
ftp>
pwd
257 "/"
```

- 4. Use the cd command, to change to a directory outside of the allowed anonymous FTP; for example, to change the directory to the /boot directory of the local file system:

```
ftp>
cd /boot
550 Failed to change directory.
```

- 5. Log out of the FTP server using the bye FTP command:

```
ftp>
bye
221 Goodbye.
```

Next'll try to connect to the FTP server using a local system account. In particular, we'll use the username yyang, which was created in a previous chapter. So let's start a sample authenticated session.

> TIP You might have to disable SELinux temporarily on your Fedora server for the following steps. Use the command setenforce 0 to disable SELinux.

- 1. Launch the command-line ftp client program again:

```
root@server -]# ftp localhost
Connected to localhost (127.0.0.1).
220 (vsFTpd 3.**)
```

- 2. Enter yyang as the FTP user when prompted:

Name (localhost:root): yyang

## 470 Linux Administration: A Beginner's Guide

- 3. You must enter the password for the user yangyang prompted:
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.

- 4. Use the pwd command to display your present working directory on the FTP server. You will notice that the directory shown is the home directory for the user yangyang.
ftp> pwd
257 "/home/yang"

- 5. Using the cd command, try to change to a directory outside of yangyang's FTP home directory; for example, try to change the directory to the /boot directory of the local file system:
ftp> cd /boot
250 Directory successfully changed.

- 6. Log out of the FTP server using the bye command:
ftp> bye
221 Goodbye.

As demonstrated by these FTP sessions, the default vsftpd configuration on our sample Fedora system allows these FTP sessions:

- Anonymous FTP access: Any user from anywhere can log into the server using the username ftp (or anonymous), with anything at all for a password. This is not the case on Debian-like distros like Ubuntu.
- Local logins: All valid users on the local system with entries in the database (the /etc/passwd file) are allowed to log into the FTP server using their normal usernames and passwords. This is true with SELinux in permissive mode. On our Ubuntu server, this behavior is disabled out of the box.

## Customizing the FTP Server

The default out-of-the-box behavior of vsftpd is probably not what you want for your production FTP server. So in this section we will walk through the process of customizing some of the FTP server's options to suit certain scenarios.

## Setting Up an Anonymous-Only FTP Server

We'll set up our FTP server so that it does not allow access to users who have regular user accounts on the system. This type of FTP server is useful for large sites that have files that should be available to the general public via FTP. In such a scenario, it is, of course, impractical to create an account for every single user when users potentially number into the thousands.

Fortunately for vsftpd is ready to serve as an anonymous FTP server out of the box. We will examine the configuration options in the vsftpd.conf file to ensure that we also disable the options that are not required.

With any text editor of your choice, open up the /etc/vsftpd/vsftpd.conf file for editing. Look through the file and make sure that, at a minimum, the directives listed next are present. (If the directives are present commented out, you might need to remove the comment [#] or change the value of the option.)

```
listen=NO
listen_ipv6=YES
xferlog_enable=YES
xferlog_std_format=YES
anonymous_enable=YES
local_enable=NO
write_enable=NO
```

You will find that those options are sufficient to enable your anonymous-only FTP server, so you may choose to overwrite the /etc/vsftpd/vsftpd.conf file (or /etc/vsftpd.conf on Ubuntu/Debian) and enter the options shown. This will help keep the configuration file simple and cluttered.

> TIP Virtually all Linux systems come preconfigured with a user ftp. This account is supposed to be a non-privileged system account and is used especially for anonymous FTP-type access. You will need this account to exist on your system in order for anonymous FTP to work. To confirm the account exists, use the getent
[root@server ~]# get passwd ftp
ftp:x:14:14:0:FTP:/var/ftp:/sbin/nologin

If you don't get similar to this, you can quickly create the FTP system account using the useradd command. To create a simple ftp user, type
[root@server ~]# -c "FTP User" -d /var/ftp -r -s /sbin/nologin ftp

If you had to make any modifications to the vsftpd.conf file, you need to restart the vsftpd service:

```
[root@server ~]# service vsftpd restart
```

## 470 Linux Administration: A Beginner's Guide

(Note: The OCR text provided in the prompt contained significant garbled text in the latter half. Based on the instructions to keep all information and correct obvious errors, I have processed the logical sections available in the first half of the document. The latter half of the provided OCR appears to be repetitive or corrupted strings that could not be reconstructed into meaningful sentences.)

```
```text
shutdown /etc/shutmsg
passwd-check rfc822 warn
```
```

Each entry defined in this file is described in detail in the man page for ftpaccess. The entries in the /etc/ftpaccess file control not only who can access the FTP server, but what they can do after a connection is made.

> > **Tip**  
> > To disable access to the FTP server to all real accounts on the system, remove the entry for real in the class line of the /etc/ftpaccess file.

The /etc/ftpusers file is used to control which users do not have access to the FTP server. By default, the following entries are placed in the /etc/ftpusers file:

+   - root
+   - bin
+   - daemon
+   - adm
+   - lp
+   - sync
+   - shutdown
+   - halt
+   - mail
+   - news
+   - uucp
+   - operator
+   - games
+   - nobody

If a username is included in the /etc/ftpusers file, that user cannot access the FTP server. If a connection to the FTP server is attempted with one username included in this file, the following message is returned:

```
```text
# ftp ftp.kcpartners.com
Connected to ftp.kcpartners.com.
220 router.kcpartners.com FTP server (Version wu-2.4.2-academ[BETA-17](1)
Wed Aug 19 02:55:52 MST 1998) ready.
Name (kcpartners.com:col): ftp
530 User ftp access denied.
Login failed.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```
```

# SHUTTING DOWN THE FTP SERVER

The ftpshut command can be used to discontinue FTP service at a given time. It provides a means of notifying users that the FTP server is temporarily shut down and that they can try again later. The ftpshut command creates a file in the /etc directory called shutmsg. When an attempt to connect to the FTP server is made, the FTP server checks for the existence of this file. If it is found, the following message is displayed:

```
```text
# ftp router
Connected to router.kcpartners.com.
```
```
```
```text
/home/ftp/etc/passwd
/home/ftp/pub
/usr/doc/anonftp-3.1
/usr/doc/anonftp-3.1/README
```
```

Installation of this package sets up everything that is required to make anonymous FTP service available. As was mentioned earlier in this chapter, in order to connect to an FTP server, you must have a user account. Even with anonymous FTP service, a user account is required. However, rather than creating a new user account for this purpose, one is already created in the /etc/passwd file. Of course it is appropriately named ftp. It’s actually a special type of user account that differs from the typical user accounts found in the /etc/passwd file. The entry for the ftp account in the /etc/passwd file is as follows:

```
```text
ftp:x:14:50:FTP User:/home/ftp:
```
```

It is the user account entry in the /etc/passwd file that allows a connection to the FTP server by anonymous users. Even though the user account entry is ftp, the user ID anonymous is accepted when connecting to the FTP server. In fact, many people mistakenly think that anonymous is the only user ID that works.

# CONTROLLING ACCESS

Access to the FTP server can be controlled in one of four ways:

+   - Removing or commenting out the FTP user in the /etc/passwd file
+   - Adding a user to exclude to the /etc/ftpusers file
+   - Removing the class of user from the /etc/ftpaccess file
+   - Shutting down the FTP server via ftpshut

The /etc/ftpaccess file is used to configure access to the FTP server. Upon initial installation, the contents of this file are as follows:

```
```text
class       all    real,guest,anonymous  *

email root@localhost

loginfails 5

readme  README*  login
readme  README*  cwd=*

message /welcome.msg          login
message .message              cwd=*

compress       yes             all
tar             yes             all
chmod           no              guest,anonymous
delete          no              guest,anonymous
overwrite       no              guest,anonymous
rename          no              guest,anonymous

log transfers anonymous,real inbound,outbound
```
```
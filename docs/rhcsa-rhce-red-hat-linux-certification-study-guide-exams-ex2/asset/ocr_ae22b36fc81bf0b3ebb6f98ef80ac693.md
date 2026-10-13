users. You can configure vsFTP through the vsftpd.conf configuration file, in the /etc/vsftpd directory.

Many standard settings in the vsftpd.conf file are different from the actual default value of a directive listed in the file. In this section, I refer to the original version of the vsftpd.conf file, as installed, as the “standard” version of the file. Before starting, there’s one critical directive not listed in the file:

```
ftp_username
```

It’s the default user for anonymous connections. In other words, when a remote user connects with username anonymous, that user connects on the server as a user named ftp. In the /etc/passwd file, that user is listed with the following settings:

```
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
```

In other words, users can’t log in directly as the user named ftp. However, anonymous users on the vsFTP server are taken to that user’s home directory, /var/ftp. So if you want to change the default directory associated with anonymous logins, change the home directory associated with the local user named ftp.

The following is an analysis of the default RHEL 6 version of this file. Some of it may be reformatted for clarity, some for desirable options. In a couple of cases, directives are analyzed in an order different from that shown in the file. First note the following comment:

```
# The default compiled in settings are fairly paranoid. This sample
# file loosens things up a bit, to make the ftp daemon more usable.
```

The vsFTP service is designed for anonymous access. The following comment emphasizes it. To disable anonymous access, you’ll have to set this to NO.

```
# Allow anonymous FTP? (Beware - allowed by default if you comment
# this out)
anonymous_enable=YES
```

The standard vsftpd.conf file supports access by users configured in the local authentication database. The RHCE objectives suggests “anonymous-only download.” To set up the server for anonymous-only access, change this option to local_enable=NO. Since that’s the default, it’s sufficient to comment out the directive as shown here:

```
# local_enable=YES
```

# 606 Part IV ♦ Implementing Network Services in SUSE Linux

Notice that the FTP server assumes a default username the same as that on the client. At this point, if you accept the default and press Return, or enter another username known to the system, you will see this:

```
530 This FTP server is anonymous only.
ftp: Login failed.
ftp>
```

But if you log in with either of the usernames ftp or anonymous, you can offer any password (traditionally this should be a valid email address, but the server will accept anything, including an empty password), and you are logged in.

```
username:/home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
Name (bible:user):ftp
331 Please specify the password.
Password:
230 Remote system type is UNIX.
Using binary mode to transfer files.
ftp>
```

If you now use ls to list files on the FTP server, you will (not surprisingly) find that there is not there:

```
ftp> ls
229 Entering Extended Passive Mode (||37477|)
150 Here comes the directory listing.
226 Directory OK.
ftp>
```

The location of the server that acts as the FTP server's root for anonymous FTP is /srv/ftp/ (just as the Apache web server's root is /srv/www/). Whatever files and directories you place there will be visible FTP. If you copy a file to /srv/ftp/, you will be able to download it by the FTP get command:

```
ftp> get afile
local: afile remote: afile
229 Entering Extended Passive Mode (||19160)
150 Opening BINARY mode data connection for afile (4096 bytes).
226 File sent OK.
ftp>
```

If you look at /var/log/messages on the server, you will see that vsftpd has logged the login:

```
Jun 25 16:41:13 bible vsftpd: Sun Jun 25 16:41:13 2004 [pid 21339] CONNECT: Client
"192.168.2.3"
```

```
Jun 25 16:41:13 bible vsftpd: Sun Jun 25 16:41:13 2004 [pid 21338] [ftp] LOGIN: Client
"192.168.2.3", anon password "password"
```

# Chapter 23 ✦ Running FTP Server on SUSE 607

Each download is also logged.
Note you can force vsftpd to write its logs to its own log file by making a small change to /etc/vsftpd.conf. Simply make sure that the following lines are present:

```
log_ftp_protocol=YES
xfer_enable=YES
vsftpd_log_file=/var/log/vsftpd.log
```

Then comment out or remove the line:
syslog_enable=YES

You can create a customized FTP banner by including a line like this in the configuration-file:

```
ftpd_banner="Welcome to our very fine FTP service."
```

When users log in using text mode FTP or a dedicated FTP client, they will see the following message before the login prompt:

```
220 "Welcome to our very fine FTP service."
Name (localhost:user):
```

This can be used to offer service messages, but is not useful for users connecting with a browser. It may be useful to include the files README and README.html, which these users can click.

You can also place a file named .message in /srv/ftp/ or any of its subdirectories. When the user changes to a directory with a file in it, the file's contents will be displayed.

```
ftp> cd pub
250-This directory contains useful files
250 Directory successfully changed.
ftp->
```

The file /srv/ftp/pub/.message contained just the line:

```
This directory contains useful files
```

vsftpd allows passive FTP connections unless you set
pasv_enable=NO

In the configuration file. You almost certainly want to allow passive connections, as otherwise many clients connecting from behind a firewall will be unable to connect.

Active FTP operates on both server port 20 (for data transfers) and port 21 (for control commands) and involves a reply connection from the server to the client, which may be blocked by a firewall behind which the client is sitting. Passive FTP involves only server port 21 and is unlikely to cause problems with a standard firewall configuration that allows established connections. For more firewall configuration, see Chapter 24.

Note that all options in the configuration file are specified in the form:

```
option=value
```

and that there should be no white space before or after the = sign.

For a standard anonymous Internet FTP download server, you have done all need to do.

# Setting Up User FTP with vsftpd

In this section we assume that you want users with accounts on the system to be able to access their home directories by FTP.

Please be aware that this could constitute a security risk if the system is available to the Internet, you should think carefully about whether you want to do it.

One common reason why you might want to do this is to set up a system to receive incoming files; you can set up "artificial" users to own each home directory for type of incoming file. You can then give the relevant usernames and passwords to each person needing the ability to upload to these directories.

You need to make further changes in the configuration file /etc/vsftpd.conf. You need to enable these lines:

```
local_enable=YES
root_local_user=YES
```

The second of these lines means that users will not be able to change directories out of their home directories. Users will be locked in a "chroot jail.".

If you now log in as a user, you will see something similar to Listing 23-1.

# Listing 23-1: Logging in to FTP Server as a User

```
user@client:/home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
```

# Chapter 23 ♦ Running an FTP Server on SUSE 609

```
Name (bible:user): user
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp: pwd
257 "/"
```

If you do not specify chroot_local_user=YES, the pwd command returns:

```
/home/user
```

You are then able to do the following:

```
ftp> cd ..
250 Directory successfully changed.
```

This enables you to access, at least in principle, the entire filesystem.

# Allowing Uploads

With the setup so far, users cannot upload to the FTP server. See Listing 23-2.

```
user:client:/home/user > ftp bible
Connected to bible.
220 (vsFtpd 2.0.2)
Name (bible:user): user
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp: put afile
local: afile remote: afile
229 Entering Extended Passive Mode (||19160)
550 Permission denied.
ftp:
```

# Listing 23-2: Attempting to Upload Files to an Server

# 610 Part IV Implementing Network Services in Linux

If you want to enable local users to upload files, you need to set the following in /etc/vsftpd.conf:

```
write_enable=YES
```

If you have done this, a new FTP session like the one shown in 23-2 will succeed in uploading to the user's home directory.

If you also want to allow anonymous logins (ftp), you need to enable the following:

```
anon_upload_enable=YES
```

There will be directories on the server allowing these writes: By default, this will not be the case. We cannot stress the dangers of allowing anonymous FTP unless you have carefully thought about what you are doing. In particular, the writable directory should not be the root of the FTP structure /srv/ftp/ You should also consider creating a writing-only setup, by creating a directory such as /srv/ftp/incoming/ owned by ftp group, and with restrictive permissions. The permissions on this directory should not allow others to write it or list it.

Listing the root directory shows:

```
root------ /srv/ftp # ls -la
d-xr------ 2 ftp ftp 144 Aug 10 17:31 incoming
```

These permissions mean that the anonymous FTP user cannot list the directory, but the FTP daemon can write to the directory, so uploading will work. The setting for the anonymous umask in the configuration file is left at its default value of 077, files that are uploaded will not be downloadable because they will have permissions 600 on the server and will not be readable by others.

If you

```
anon_umask=022
```

/etc/vsftpd.conf, then files that have been uploaded are anonymous-downloadable, although the incoming directory is still listable. This is almost very undesirable, except in a trusted environment, because confederates of anyone who has posted files on your server will be able to download them.

The root FTP directory /srv/ftp/ itself should be owned by user root and group root, and there should be no subdirectory that is readable, writable, and listable.

See Chapter 2 for more information about permissions.

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_654_0.png)

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
The PASV data connection method is enabled to let external users know the IP address of the FTP server. This is a common problem when using FTP from behind a firewall/gateway that uses IP masquerading or when incoming data connections are disabled. For example, here is a connection to an FTP server (running ProFTPd), an attempt to view a directory listing, and the resulting need to use ftp's internal passive command:

```
$ ftp ftp.tux.org
Connected to gwyn.tux.org.
220 ProFTPD 1.2.5src1 Server (ProFTPD on ftp.tux.org) [gwyn.tux.org]
500 AUTH not understood.
KERBEROS_V4 rejected as an authentication type
Name (ftp.tux.org:gbush): gbush
331 Password required for gbush.
Password:
230 User gbush logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd public_html
250 CWD command successful.
ftp> ls
500 Illegal PORT command.
ftp: bind: Address already in use
ftp>
ftp> pass
Passive mode on.
ftp> ls
227 Entering Passive Mode (204,86,112,12,187,89).
150 Opening ASCII data connection for file list
-rw-r--r-- 1 gbush gbush 8470 Jan 10 2000 LinuxUnleashed.gif
-rw-r--r-- 1 gbush gbush 4407 Oct 4 2001 RHut72d.gif
-rw-r--r-- 1 gbush gbush 6732 May 18 2000 SuSEUnleashed.jpg
-rw-r--r-- 1 gbush gbush 6175 Jan 10 2000 TYSUSE.gif
-rw-r--r-- 1 gbush gbush 3135 Jan 10 2000 TZones.gif
```

> NOTE
> Browse to http://slacksite.com/other/ftp.html for a detailed discussion regarding active and passive FTP modes and the effect of firewall blocking of service ports on FTP server and client connections.

Another default setting is that specific user login controls are not set, but you can configure the controls to deny access to one or more users.
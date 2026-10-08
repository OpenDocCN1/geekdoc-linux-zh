
[content]
# 456 ANONYMOUS FTP SERVERS

should not specify a system directory.

- PATH_PIDNAMES "/var/run/ftp.pids-%s"
Users are subdivided into different classes (for example, users in the local domain and other users). For each class, restrictions can be entered and monitored, this is done using these files.

- PATH_CVT "/etc/ftpconversions"
The ftp daemon can pack or unpack files during the transfer. For this purpose, the appropriate programs must be present in ~ftp/bin/ftp-exec and the file /etc/ftpconversions must be set up accordingly.

- PATH_XFERLOG "/var/log/xferlog"
This file stores the transmission statistics, which you can evaluate, for example, with awk or perl. You should check this file regularly for unusual events.

- PATH_PRIVATE "/etc/ftpgroups"
This is the password file for the site group and site gpass commands.

- PATH_UTMP "/var/run/utmp"
This specifies the path to the utmp file, which contains the names of the users currently logged into the system. You can then use the usual UNIX commands (for example last) to find out which of these users are currently using the ftp server.

- PATH_WTMP "/var/log/wtmp"
This specifies the path to the wtmp file. This file contains a log of the user logins.

- PATH_LASTLOG "/var/log/lastlog"
This file contains the data of the last login of a user.

Finally, you will need to check the settings in the files /src/config/config.lnx and ./src/makefile/Makefile.lnx. Subsequently, you can compile the daemon with ./build lnx. After a short time, you will find the programs in the subdirectory /.bin, and you can terminate the installation with ./build install.

To activate the new daemon, you need to modify the file /etc/inetd.conf and re-initialize the inetd server with the signal SIGHUP. This is done by means of the command killall -HUP inetd. Subsequently, the ftp daemon is available for users of this computer. The setup of an anonymous ftp server is described in the next section.

## 18.2 Administration of an anonymous ftp server

An ftp server, more than other services, raises some security problems. Some are statically taken into consideration in the implementation of the ftp daemon. Many other issues affect the security of your server. Before you make the server available to other users, you should take time to read the pages and the CERT advisories on this subject.

To keep programs as small as possible, LINUX normally uses shared libraries. After the chroot to the ~ftp directory, access to the libraries stored in /lib is no longer possible. Therefore you must copy either the required libraries (ld.so and libc.so) together with the files from /etc (ld.so.cache, group, and passwd) into the ~ftp/lib directory, or you must use statically linked programs, which as a rule would be the simplest solution.

For a simple ftp server without special features you will only need the ls program. If you want to provide automatic packing of directories and files, you will also need tar and compress gzip. These programs must be copied into the directory ~ftp/bin/ftp-exec. Additional programs that ftp users are allowed to execute by means of the site exec command must be copied into the ~ftp/bin/ftp-exec directory. Here, one frequently finds a search program for the file index. Use special care when deciding commands alien users are allowed to execute on your computer.

When setting up the server, you must ensure that you do not make any files or directories writable for alien users. The only exception should be the incoming directory. Transmissions into or from this directory are often misused as intermediate storage for pirate copies or other illegal method.

To display the file name, the ls program needs the files ftp/etc/passwd and ftp/group. You should not, however, use the system password file, but an especially elaborate one in which no passwords are stored. If you wish, you can also change the user IDs (and their names) to prevent them from being revealed to the world.

In the next step, you can set up the special functions of the server in the files ftpconversions, ftpusers, and ftpgroups. In the file /etc/ftpconversions, you can specify which conversions can be carried out during the transfer and which programs can be used for that purpose. Each line of this file consists of eight colon-separated columns that describe one conversion method. An example is shown in Listing 18.1.

```
:Z : : /bin/compress -d -c Xs:T_REG:O_UNCOMPRESS:UNCOMPRESS
: .:2:/bin/compress -c Xs:T_REG:O_COMPRESS:COMPRESS
:.gz: : /bin/gzip -cd Xs:T_REG:O_UNCOMPRESS:GUNZIP
: :gz:/bin/gzip -9c Xs:T_REG:O_COMPRESS:GZIP
: :tar:/bin/tar -cf - Xs:T_REG|T_DIR|O_TAR:TAR
: :tgz:/bin/tar -czf - Xs:T_REG|IT|T_DIR|O_TAR:TGZ
```

### 18.1 The file /etc/ftpconversions.

The meaning of the individual fields is shown in Table 18.1. Please note that the prefix options are not yet implemented. You must copy the required programs (statistically linked, if needed) into the directory.

| Field | Description |
|---|---|
| 1 | Name prefix |
| 2 | Name suffix |
| 3 | Name prefix |
| 4 | Name suffix |
| 5 | Command |
| 6 | Types: T_REG, T_DIR |
| 7 | Options: O_COMPRESS, O_UNCOMPRESS |
| 8 | Description |

The meaning of the individual fields is shown in Table 18.1. Please note that the prefix options are not yet implemented. You must copy the required programs (statistically linked, if needed) into the directory.

In the file /etc/ftpconversions, you can specify which conversions can be carried out during the transfer and which programs can be used for that purpose. Each line of this file consists of eight colon-separated columns that describe one conversion method. An example is shown in Listing 18.1.

## 18.3 ADMINISTRATION OF AN ftp SERVER

An ftp server, more than other services, raises some security problems. Some are statically taken into consideration in the implementation of the ftp daemon. Many other issues affect the security of your server. Before you make the server available to other users, you should take time to read the pages and the CERT advisories on this subject.

To keep programs as small as possible, LINUX normally uses shared libraries. After the chroot to the ~ftp directory, access to the libraries stored in /lib is no longer possible. Therefore you must copy either the required libraries (ld.so and libc.so) together with the files from /etc (ld.so.cache, group, and passwd) into the ~ftp/lib directory, or you must use statically linked programs, which as a rule would be the simplest solution.

For a simple ftp server without special features you will only need the ls program. If you want to provide automatic packing of directories and files, you will also need tar and compress gzip. These programs must be copied into the directory ~ftp/bin/ftp-exec. Additional programs that ftp users are allowed to execute by means of the site exec command must be copied into the ~ftp/bin/ftp-exec directory. Here, one frequently finds a search program for the file index. Use special care when deciding commands alien users are allowed to execute on your computer.

When setting up the server, you must ensure that you do not make any files or directories writable for alien users. The only exception should be the incoming directory. Transmissions into or from this directory are often misused as intermediate storage for pirate copies or other illegal method.

To display the file name, the ls program needs the files ftp/etc/passwd and ftp/group. You should not, however, use the system password file, but an especially elaborate one in which no passwords are stored. If you wish, you can also change the user IDs (and their names) to prevent them from being revealed to the world.

In the next step, you can set up the special functions of the server in the files ftpconversions, ftpusers, and ftpgroups. In the file /etc/ftpconversions, you can specify which conversions can be carried out during the transfer and which programs can be used for that purpose. Each line of this file consists of eight colon-separated columns that describe one conversion method. An example is shown in Listing 18.1.

| Additional Information and Sources |
|---|---|
| Man pages: | ftppd(8), ftpaccess(5), ftposts(5), xferlog(5), ftpwho(1), fthut(8), ftpconversions(5) |
| ftp server: | sunsite.unc.edu |
| ftp path: | /pub/Linux/System/file-transfer |
| File name: | wu-ftppd-2.4.tar. |
| Size: | about 185 Kbytes |
| Mailing list: | wu-ftppd-announce, subscribe with email to listproc@mail.wustl.edu without subject with subscribe list name |

[content]

All TCP/IP-based protocols and applications discussed until now are a standard for UNIX systems of all. In UNIX networks, these protocols are usually sufficient. Things change, however, if a UNIX system is to be linked into an existing local network composed of PCs and Macintosh systems. There, you often find an unruly growth of protocols, and each computer is supposed to communicate with every other directly and as little effort as possible.

Besides the TCP/IP protocol, LINUX speaks a number of languages widely used in local networks. LINUX proves to be an economical and powerful solution for connection of different network platforms. Comparable commercial packages are often prohibitively expensive for smaller businesses or private users.

A widely used protocol in PC networks is the IP protocol (Internet Packet Exchange) by Novell NetWare. Usually, powerful PCs are used as servers; the speed is much higher than with TCP/IP, which is why this protocol is very popular in pure PC networks. Clients exist for DOS, Windows, OS/2, and MacOS, either included in the operating system or available from Novell.

Novell offers a TCP/IP package for its servers, but it does not attain the functionality of a UNIX host. Furthermore, this package, also includes NFS, is relatively expensive. With IntraNetware, Novell too is slowly opening its doors to TCP/IP-based networking.

Another protocol is Server Message Block (SMB). This is used by the LAN manager (by IBM and Microsoft) and by Windows NT, Windows for Workgroups, and Windows 95. Under Linux, the samba package is used as a server running SMB over TCP/IP. This package can also be employed on many other UNIX platforms. As a client, you can use the smb file system for


permit only the retrieval of files from the server. Although many users today are unaware of FTP, it remains an important protocol because web pages frequently link to binary files stored on FTP servers. One important drawback to FTP is that it's entirely unencrypted, so passwords and data aren't very secure.

**NFS servers**
NFS was developed by Sun Microsystems as a means of file sharing among UNIX systems. NFS supports all the usual UNIX filesystem features, such as ownership and permissions, so it's long been the file sharing protocol of choice on UNIX and UNIX-LIKE systems. NFS relies upon a *trusted hosts* security model, in which the server relies upon the client to authenticate users and control access to files. This model was reasonable in the days when UNIX computers were relatively rare and tightly controlled, but it's riskier in today's environment. Thus, proper control of NFS servers, including very careful access control restrictions, is important.

**SMB/CIFS servers**
SMB/CIFS is most commonly used on Windows-dominated networks for file and printer sharing. The protocol supports DOS and Windows filesystem features, but not UNIX filesystem features. Samba provides elaborate mechanisms to support these features on UNIX-style systems. In fact, in many respects Samba is more flexible than the SMB/CIFS server support built into Windows, which can make a FreeBSD system a valuable addition to a Windows-dominated network. SMB/CIFS uses usernames and passwords for access control. The password may optionally be encrypted, but other data are not.

**AppleTalk servers**
Apple developed a file-sharing protocol called *AppleTalk* for use with its Macintosh computers. You can turn FreeBSD into an AppleTalk server with the Netatalk package (http://netatalk.sourceforge.net). This package is most useful for versions of Mac OS prior to Mac OS X, so I don't describe it in any detail in this book. Mac OS X is built around a UNIX core (including substantial borrowing from FreeBSD), so it can use NFS for file sharing, as well as AppleTalk and SMB/CIFS. Like UNIX-style systems, AppleTalk uses a username/password model for authentication, and the password may or may not be encrypted, depending upon settings on the client and server.

**rcp servers**
The rcp program is a very simple file-transfer tool. It works much like the ordinary cp program for copying files locally, but it's network-enabled. Like NFS, rcp relies upon a trusted-hosts security model, with access controls provided in users'.rhosts files. This tool can be a quick and convenient way to transfer files, but it's not very good for browsing files on a remote server.

**SSH servers**
The Secure Shell (SSH) program is generally considered a remote login server, and is described in Chapter 21. It includes the ability to transfer files, though. This can be done via the scp client program, which works much like rcp. More recently, SSH file-transfer client programs have been acquiring FTP client features, and in some cases the two have merged. The sftp and GFTP clients, for instance, both provide FTP-like interfaces but support encrypted data transfers via an SSH server. (In fact, gFTP was originally an FTP client, and can still function as one.)

## Web servers

Web servers, which use the Hypertext Transfer Protocol (HTTP), are designed primarily for one-way delivery of data files, from the server to the client. They can transfer files in the other direction, though. Web servers typically don’t use authentication, although they can. Because web servers typically deliver files that the user reads immediately in the web client program (the web browser), and because web servers are so important, Chapter 20 describes the configuration of the most popular web server, Apache.

Typically, FTP servers are used for cross-platform data transfers or when there’s little need for clients to dynamically alter data stored on the server. They can be used with authentication (to give individual users access to their files), but this practice is risky because of the unencrypted nature of the FTP password exchange. You may want to shift to SSH for such functions, if possible. (No special SSH server configuration is required.)

File sharing servers are most commonly used with clients of the target OS types (UNIX or UNIX-like systems for NFS; DOS, Windows, or OS/2 systems for Samba; and Mac OS systems for Netatalk). In a few cases, though, you may want to use a protocol built for another OS, such as NFS with Windows clients. You might do this because a network is dominated by one type of system and you have only one or two instances of another type, thus making it simpler to equip the client computers with appropriate client protocols. You might also do this if the security model of the protocol better fits your network’s security policies.

## Setting Up an FTP Server

Basic FTP server configuration in FreeBSD is fairly straightforward, but if you want to run something other than the standard BSD FTP server, or if you want to run a more advanced configuration (including an anonymous FTP server), you’ll have more work to do. Consult the documentation for the alternative server to learn more about such configurations. Actually running the server requires making changes to your inetsd super server configuration, as described in Chapter 16. Making changes to the configuration requires altering the options used when launching the server from inetsd.

## Common FTP Server Programs

FTP has been around for long enough that several FTP server programs have cropped up. Some of the options in FreeBSD are

- **BSD FTP** The default FTP server in FreeBSD traces its ancestry back to the 4.2 BSD release. This server is fairly simple to configure and is installed by default on most FreeBSD systems.
- **WU-FTPD** The WUarchive FTP Daemon (WU-FTPD; [http://www.wu-ftpd.org](http://www.wu-ftpd.org)) is a popular FTP server on many platforms, but it’s not commonly used in FreeBSD. It has a history of security-related bugs.
- **ProFTPd** This package, headquartered at http://proftpd.linux.co.uk, is designed as a very flexible and extensible FTP server. Its configuration file syntax is based on that used by the Apache web server.
- **oftpd** This program is a small FTP server that’s designed for security when running an anonymous FTP site. You can learn more about it at http://www.time-travelers.org/oftpd/.
- **twoftpd** This is another FTP server that’s designed for simplicity and security. Unlike many FTP servers, it can’t run external commands, and it uses the `chroot()` system call to lock itself into the user’s home directory once a user logs in.

All of these servers are available as packages or in the ports system, except for BSD FTP, which is installed with the base FreeBSD system. One of the reasons for the large number of available FTP servers is that WU-FTPD, which has long been a popular FTP server, has garnered a reputation for security-related bugs. Thus, many independent projects have cropped up to develop more security-conscious FTP servers. The default FreeBSD FTP server doesn’t have a bad reputation in this respect. If you want something with more features, ProFTPD may be worth investigating. Other servers (including some not listed here—check the ftp ports directory or package section) may provide features that meet particular unusual needs, such as advanced access control features or the ability to process data as it’s transferred.

### Running an FTP Server

As described in Chapter 16, servers can be started through startup scripts or run from a super server. FTP servers are frequently, but not universally, run in the latter manner. In the case of FreeBSD, the standard `/etc/inetd.conf` file includes an entry for running the BSD FTP server, but it’s commented out by default:

```
#ftp stream tcp nowait root /usr/libexec/ftpd ftpd -l
```

To enable the FTP server, you should:

1. Remove the pound sign (#) that begins the line.
2. Restart inetd by typing `killall -SIGHUP inetd`.

At this point, an attempt to access the computer’s FTP server from another system should be greeted by an FTP login prompt, assuming no firewall or other access control tool blocks the FTP port. For instance:

```
$ ftp halrioprilillar
Connected to halrioprilillar.rodbooks.com.
220 halrioprilillar.rodbooks.com FTP server (Version 6.00LS) ready.
```

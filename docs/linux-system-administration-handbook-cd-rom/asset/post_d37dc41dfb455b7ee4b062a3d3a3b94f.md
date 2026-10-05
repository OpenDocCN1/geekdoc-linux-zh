
# Newsgroups

```
news.admin.technical
news.software.nntp
the comp.os.linux groups
```

# Mail Addresses

```
bugs@isc.org
```

# 10.9 Summary

For many users, getting access to NetNews provides a source of information on a large series of subjects. But many Linux setups do not have the spare disk space to handle a full feed. In this case, you may only want a partial feed to handle the newsgroups that would be most beneficial to your users. Plan ahead for the disk space and time needed to maintain a feed before getting a feed.

# Setting Up FTP 11

Virtual, anonymous and more.

The File Transfer Protocol (FTP) is one of the most frequently used services available on the Internet. Setting up an anonymous FTP server is fairly straightforward. Other services, like virtual FTP hosts and ftp-only accounts, are a little more tricky.

We'll cover how to set up all of these services in this chapter and then talk about a few client programs.

# 11.1 Anonymous FTP

This is the most common service: a single anonymous FTP server on a machine. Most Linux distributions will set up this up automatically. Typically the ftp root will be `/home/ftp`.

If, for some reason, anonymous FTP isn't set up on your machine, it is very simple to set up.

# Setting Up Anonymous FTP

In the instructions below, ~ftp is the home of the anonymous ftp user as specified in the /etc/passwd file.

The FTP daemon, vsftpd, recognizes the anonymous user and adjusts some aspect of the account. The root directory for access is set to ~ftp. This means that access is limited to the directories and files in ~ftp at best. Permissions can, of course, restrict access further. Because the file system root is changed, several directories and files need to be set up to allow a minimal level of functionality.

- ~ftp should be owned and only writable by root.
- ~ftp/bin should also be owned and only writable by root. It should contain the ls program (located at /bin/ls). ~ftp/bin/ls should be owned by root and have the mode ---x--x--x, chmod 111 ~ftp/bin/ls is if this is not the case.
- ~ftp/lib should contain ld-linux.so.1, ld.so and libc.so.5. These can be found in /lib.

If you want listings translate user and group IDs into names, you will need to create ~ftp/etc. It should have mode 755 and contain passwd and group files that associate IDs with names. The encrypted password field is not used and should be empty. The only fields that to be present are username, UID, and GID.

The upload and download directory ~ftp/pub should have mode 755 and own by ~ftp. This will allow others to upload and read from the directory. You can course change ownership and permissions to allow the level of access you desire.

The user "~ftp" should have an entry in /etc/passwd similar to this:

```
ftp*:14:50:FTP User:/home/ftp:
```

FTP is a service controlled by inetd and, such, requires an entry in /etc/services. Once again, this should be set up already, but if it is not, add an entry like this:

```
ftp 21/tcp
```

# 11.2 FTP Access for User Accounts

When someone connects with a username other than anonymous (or its alias ftp), three conditions must be met for access to be granted. The username and (non-null) password combination must be valid. The username must not be present in /etc/ftpsusers. The user must have a valid shell, that is, it must be listed in /etc/shells.

# 11.3 FTP-only Accounts

It is possible to set up user accounts that can be accessed only via FTP. These accounts barely behave similarly to the anonymous account and can coexist peacefully with it. Since the directory root is reset, you will need to set up the bin, lib, and etc directories as they are set for the anonymous account.

To restrict particular accounts to FTP-only access you need to edit (or possibly create) the /etc/ftpaccess file.

The example below sets up two users, ftpbob and jane, as FTP-only accounts.

```
#
# /etc/ftpaccess
#
class all real,guest, anonymous *
class ftponly ftpbob, jane *

loginfails 5

readme README* login
readme README* cwd=*

message /welcome.msg login
message .message cwd=*

compress yes all
tar yes all
overwrite yes real
chmod guest, anonymous
delete no guest, anonymous
rename no guest, anonymous
overwrite no guest, anonymous

grouproup ftponly
```

# Chapter 11 • Setting Up FTP Services

The class line sets up groups of users and a host pattern to match against the remote host. The “* matches all hosts.

The corresponding /etc/passwd entries are

```
jane:9phhxXoQW:518:518:Jane's FTP-only Account:/a/ftp/jane:/bin/false
ftpbob:I8Leijehfp:518:518:Bob's FTP-only Account:/a/ftp/ftpbob/incoming:/bin/false
```

The shells for the two users are both valid that will deny them shell access. The home directory will be the root directory for the ftp session. Additionally, the ftpbob account will be chdir() into /a/ftp/ftpbob/incoming.

You probably noticed that the ftpprocess sets up a number of other parameters as well.

The “real” word is a keyword for any valid account, “anonymous” stands for any anonymous account, and “guest” refers to guest level access.

The compress and tar entries set ftppd when to allow on-the-fly (de)compression or (un)tarring.

The README and message entries set up patterns to search for files to be automatically displayed (message) when connecting and entering directories (README).

In the above example, low-access accounts (anonymous and guest) are forbidden from deleting, changing the mode of, or renaming files.

loginfails does what you expect it to do: Drop the connection after the specified number of failed login attempts.

# 11.4 Virtual FTP Hosts

Virtual FTP is frequently used by ISPs to set up FTP services for multiple domains on one server. The stock Linux ftppd does not support virtual FTP hosts. The stock Linux ftppd does not support virtual FTP hosts. You will need to use virtual hosting.

# 11.5 FTP Clients

There are two types of ftp clients: those which support user-based FTP dhose which support only anonymous FTP.

Today, probably the most common way to access anonymous FTP sites is with a Web browser. These are typically the only clients that only support anonymous FTP.

There are also a number of other FTP clients ranging from the simple command line like the ftp program to full-screen clients like NcFTP to graphical clients like XFTP.

# ftp

The ftp program is a command-line-based program. It is not particularly friendly but should always be available on any Linux (or UNIX system).

# NcFTP

NcFTP is a full-screen (still ASCII) ftp client. It sports a number of features, including

- A list of shortcuts for FTP hosts including storage for username and passwords (if so desired) for each host (see Figure 11–1).

![](img/cd7585e53abd949068548271c07fcdd8_169_0.png)

Figure 11–1 A list of shortcuts for FTP hosts.

- Automatic connection as anonymous (sends “anonymous” as the user-name and a string you supply as the password; the anonymous FTP password is stored in the rc file in your home directory).
- The screen is split into a command typing area and an output area (see Figure 11–2).

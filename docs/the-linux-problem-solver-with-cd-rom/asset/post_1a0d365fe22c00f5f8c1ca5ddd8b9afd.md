
```
print command = send_job_command -Pmyprinter %s
lpq command = /usr/bin/lpq -Pmyprinter
lpm command = /usr/bin/lprm -Pmyprinter %j
path = /tmp
```

Here, whatever you specify as send_job_command sends jobs to the printer. You may want to do this in order to bypass a print filter or add a different filter. Relevant man pages: lpr (1), lpq (1), lprm (1), lpd (8)

## Filesharing

You can export directories to Windows clients in SAMBA's smb.conf file in two ways. One is with a regular section, and the other involves the special [homes] section. Here is a very simple single-path share in a regular section:

```
[projects]
path = /stage/projects
valid users = +staff
writeable = yes
```

Here, we're allowing read-write access to /stage/projects for the users in the group staff. To use /stage/projects as a network drive on a Windows machine, you can enter the following at an MS-DOS command prompt:

```
net use g: \\SERVER\PROJECTS /user:username
```

Here, SERVER is the NetBIOS name of the SAMBA server and username is a user in the group staff. We're also assuming that g: isn't currently in use. Similarly, you can attach a network drive by right-clicking on the My Computer icon on a Windows machine, then selecting Map Network Drive on the menu.

## Name Alterations

Because of the limitations of DOS-style file names, SAMBA presents file names differently than they actually appear in the Unix filesystem. By no coincidence, SAMBA calls this name mangling. You end up with a name like XINIT~3L.193 because Windows can't handle a really long name.

There are two ways to ask for a home directory from a SAMBA server. The first is explicit, as in this DOS command:

```
net use g: \\SERVER\username1 /user:username2
```

When you make this request, the SAMBA server on SERVER first looks at the username1 part of \\SERVER\username1 as it normally would in any other section in smb.conf. If username1 matches any other section, this matching section is used. However, if it does not match and there is a [homes] section, SAMBA makes one more attempt before returning an error: It looks up the home directory of username1, which becomes the share if that username1 is a user on the SAMBA server. username2 is the Linux user to connect as (usually the same as username1).

The other way to ask for a home directory share is implicit:

```
net use g: \\SERVER\homes /user:username
```

Here, you’re telling SAMBA straight away that you want your home directory and that your login is username. A fairly safe example for a [homes] section is:

```
[homes]
guest ok = no
browseable = no
```

It’s up to you whether you want users to be able to write to the directories (using the writable parameter). The file permissions go down to the underlying Unix filesystem on the SAMBA server; the SMB client can only write to the files and directories that the connecting user can write to.

Once you look at a user’s share, it shows up in the shares list. If you don’t like the way the [homes] section works, you can set up a simpler one, like this:

```
[u]
guest ok = no
path = /home/%u
```

Any access to \\SERVER\%u results in the home directory of the account used to connect (this example assumes that all of your home directories are in /home).

## SAMBA Clients

SAMBA comes with a program called smbclient. It’s useful for occasional remote access purposes, as well as for debugging your own SAMBA server’s smb.conf file. Use it as follows:

```
$ smbclient '\\SERVER\share'
```

You can employ -U user to change the user (the default is your log-in name). It asks you for a password unless you specify the -P passwd option. If you're trying to access a guest share, you can specify an empty password or just press ENTER at the password prompt. Upon success, smbclient gives you a prompt like this:

```
Domain=[MYWRKGRP] OS=[Unix] Server=[Samba 2.0.6]
smb: \>
```

From there, you can use commands similar to ftp's put, mput, get, mget, and so on. Use help to get a full list.

If you want to use shares on Windows machines on a regular basis, you should consider the SMB filesystem available in the Linux kernel. To use it, first get your kernel to support smbfs by either compiling it into the kernel or building and loading it as a module (the latter option is preferable—see Chapter 7). Then look in your SAMBA package for an smbmount program that combines the smbclient and mount programs:

```
# smbmount '\\SERVER\SHARE' -c 'mount /mnt' -U user -P password
```

Relevant man pages: smbclient (1), smbmount (8)

## 4.3 Netatalk

To get your Linux machine to speak AppleTalk, you need two things: kernel support for AppleTalk low-level protocols, and the server programs that provide services (such as filesharing and printing) to clients. AppleTalk has a number of low-level protocols (transport mechanisms), but the most common on local networks is DDP running over Ethernet. There's a kernel configuration option for this under "Networking options"; it's called AppleTalk DDP, and you should configure it as a module as described in Chapter 7.

The Netatalk package deals with the services. Its main facilities are file-sharing and printing for servers and clients, but it also includes a few utilities for looking up names and converting Macintosh-style files. The original Netatalk package has not been modified for some time, but a new version with many enhancements called Netatalk-asun is now available. This book assumes you have the enhanced package. In addition to the version on the included CD-ROM in support/atalksamba, you'll find it (at least at the time we wrote this book) at ftp://ftp.u.washington.edu/public/asun/.

Unfortunately, Netatalk's included documentation is on the skinny side; the manual pages only describe command-line options, with very little description of configuration files.

After you've built the AppleTalk kernel module (appletalk.o), use insmod on it. The kernel generates a message such as this:

```
NET4: AppleTalk 0.18 for Linux NET4.0
```

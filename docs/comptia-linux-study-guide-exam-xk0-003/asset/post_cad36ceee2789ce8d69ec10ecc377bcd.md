
particularly if you compile Samba yourself. You can also use the `passdb` backend option to alter how Samba stores its encrypted passwords; consult the `smb.conf` man page for details.) To add a user to the Samba password database, pass `smbpasswd` the `-a` parameter and the username:

```
# smbpasswd -a john
```

This command creates an entry for **john**, provided that the local Linux user **john** already exists. (The `smbpasswd` program will create entries only for those users who already have standard Linux accounts.) When you type this command, you’ll be prompted twice for a password, much as when you use the Linux `passwd` command to change a password. In fact, you can then use `smbpasswd` to change Samba passwords for existing users.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_515_0.png)

> The first time you use the `smbpasswd` command, it will complain about the lack of an `/etc/samba/smbpasswd` file. This complaint looks like an **error** message, but the utility creates the file, so nothing is wrong or needs your attention.

### Resolving Hostnames in Samba

SMB/CIFS was originally built around non-TCP/IP networking, but today’s implementations generally use TCP/IP. The result can be a bit confusing when it comes to name resolution, since implementations differ in how they resolve names—some use TCP/IP hostnames, but others use NetBIOS names, even when working over TCP/IP.

To maximize flexibility, Samba supports a file called `lmhosts`, which is typically stored in `/etc/samba`. This file is similar to the Unix `/etc/hosts` file, in that it provides a mapping of hostnames to IP addresses. It consists of one line per host, with an IP address and hostname:

```
172.24.21.34 DANCE
```

This line maps the NetBIOS name `DANCE` to `172.24.21.34`. If you have problems locating Windows servers using Samba clients, editing `lmhosts` may fix the problem. Sometimes, though, this file will be useless. In particular, if your servers’ IP addresses change frequently (say, because you’re using DHCP with dynamic IP addresses to configure them), then a static `lmhosts` file will go quickly out-of-date. In that case, the standard NetBIOS name resolution should be used. Samba tries to do this by default, but to be sure, check the `[global]` section of your `smb.conf` file for the **name resolve order** directive:

```
name resolve order = host lmhosts wins bcast
```

Each subsystem is tried in the order listed. If a subsystem is omitted from the list, it’s not used. In this example, **host** uses Linux’s standard DNS lookup, **lmhosts** uses the `lmhosts` file, **wins** uses a NetBIOS equivalent to a DNS server, and **bcast** uses low-level broadcast lookups that are unique to SMB/CIFS. Try different orders of these four options until you find a combination that works.

# Sharing Files with Samba

To share files with Samba, you must create file share definitions. These can be as simple as a share name in square brackets in the `smb.conf` file:

```
[sample]
```

This line creates a share called SAMPLE. If no other lines are present until the end of the file or the next share definition, the share is read-only and provides access to the `/tmp` directory. To make the share useful, chances are you'll want to change at least some of these defaults:

```
[sample]
     comment = Sample Samba Share
     path = /home/samba/sample
     read_only = No
```

This example sets three parameters. The `comment` line sets a comment string that's associated with the share and that appears in many clients' network browsers. It doesn't directly affect the share's functionality, but providing a descriptive comment can help users find the shares they need. The `path` parameter tells Samba what directory to share. The default value is `/tmp`, but that's not usually very useful. A synonym for this parameter is `directory`. Finally, setting `read_only = No` tells Samba that users may write to the share. The `writeable`, `writable`, and `write_ok` parameters are antonyms for `read_only`; that is, `writeable = Yes` is equivalent to `read_only = No`. An important caveat about Samba's write permissions is that they still work within the constraints of Linux file permissions, as described in Chapter 2. Every user who accesses a Samba server does so as an ordinary user. If that user can't write to a directory or file, Samba won't permit the user to do so (at least, not without using more advanced parameters). Thus, you must ensure that permissions are set appropriately within file shares if you want your users to be able to write to them. In fact, permissions must be set to enable users to read files in shares that they should be able to read, as well. In most cases, 0644 (r-w-r-r-r--) permissions do nicely for files in read-only shares, but managing permissions in read/write shares can be complex.

An important special Samba share is the `[homes]` share. Unlike most shares, this one doesn't point to a single directory; it points to the user's home directory, as defined in `/etc/passwd`. If you want users to be able to store their personal files on a Samba server, a `[homes]` share can be just the thing you need. Most `smb.conf` sample files include a working `[homes]` share, so you might not need to do anything to add one. In operation, this share appears as the user's username---for instance, the user john sees a share called john.

> Samba is a very complex and powerful server, and this description barely presents the most basic Samba information. If you need to do more with Samba, you should consult its copious documentation or a book on the subject, such as my Linux Samba Server Administration (Sybex, 2001).

# Sharing Printers with Samba

In addition to file shares, Samba supports printer shares. The simplest way to share printers is with a `[printers]` share, which is analogous to a `[homes]` share in that both share every available instance of their type (printers or user home directories, respectively). A typical `[printers]` share definition looks like this:

```
[printers]
    comment = 'All Printers'
    path = /var/spool/samba
    print ok = Yes
```

A share called `[printers]` causes all the printers defined on the Samba server to be shared with SMB/CIFS clients. This definition depends on Samba to be able to identify the printers. On a Linux system that uses the Common Unix Printing System (CUPS) for printing, you should normally include a line that reads `printing = cups` in the `[global]` section in order to tell Samba how to interface with the printing system.

Instead of, or in addition to, a `[printers]` definition, you can create named printer-by-printer definitions. These, like the `[printers]` share, must include the `print ok = Yes` parameter or its synonym, `printable = Yes`. By default, Samba looks for a local printer with the same name as the printer share; however, you can point Samba to a different share by using the `printer name` parameter, as in `printer name = laser` to print to a local queue called `laser`.

Print jobs accepted by Samba are submitted to the Linux printing system as if they were locally generated. In most cases, this means that clients should be configured as if they were printing to a PostScript printer, even when the printer isn't a PostScript model. Generic PostScript drivers usually work well, as do drivers for Apple LaserWriter printers. For color printers, try using a driver for a QMS magicolor printer; these drivers usually work well with Samba. Some printer queues' smart filters recognize native printer languages and pass such files through unmodified. If this is the case, using the drivers provided by the printer manufacturer will work. Ultimately, you may need to experiment to determine what works well on the client side.

# Using a Windows Domain

Most networks that rely heavily on SMB/CIFS for file sharing deploy a domain configuration, which differs from the simpler workgroup configuration in several ways. The most important of these is that a domain includes a *domain controller* computer, which manages accounts for all the computers on the domain.

If you want to use a Windows domain with your Samba server (or Linux SMB/CIFS clients), you must set a couple of `smb.conf` global options:

```
security = Domain
password server = 172.24.21.98
```

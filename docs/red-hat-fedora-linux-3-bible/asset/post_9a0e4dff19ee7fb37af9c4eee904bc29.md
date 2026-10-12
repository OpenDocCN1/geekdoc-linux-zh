
```
$ smbclient -L localhost
Password: *********
Domain=[ESTREET]  OS=[Unix]  Server=[Samba 3.0.3-4]

Sharename       Type      Comment
---------       -----     -------
homes           Disk      Home Directories
IPC$            IPC       IPC Service (Samba Server)
ADMIN$          Disk      IPC Service (Samba Server)
hp-ns1          Printer
Domain=[ESTREET]  OS=[Unix]  Server=[Samba 3.0.3-4]

Server          Comment
------          -------
PINI            Samba Server
MAPLE           Windows XP
NSI             Samba Server
Workgroup       Master
---------       -------
ESTREET         PINI
```

This shows that the Samba server is running on the local computer. Shared directories and printers, as well as servers in the workgroup, appear here. If the Samba server is not running, you will see *Connection refused* messages. You need to start the Samba service as described in the "Starting the Samba service" section earlier in this chapter.

## Firewall open?

If the Samba server is running, it should begin broadcasting its availability on your LAN. If you try to access the server from a Windows or Linux client on your LAN, but get a *Connection refused* error, the problem may be that the firewall on your Linux Samba server is denying access to the NetBIOS service. If you have a secure LAN, you can type the following (as root user) to flush your firewall rules temporarily:

```
# iptables -F
```

Then, try to connect to the Samba Server from a Windows or Linux client. If you find that you can connect to the server, turn the firewall back on:

```
# service iptables restart
```

You then need to open access to ports 137, 138, and 139 in your firewall so that the Samba server will be able to accept connections for services. (See Chapter 14 for information on modifying your firewalls.)

## User passwords working?

Try accessing a shared Samba directory as a particular user (from the local host or other Linux system on your LAN). You can use the `smbclient` command to do this. Here’s an example:

```
# smbclient //localhost/tmp -U chris
added interface ip=10.0.0.1 bcast=10.0.0.255  nmask=255.255.255.0
Password: ******
Domain=[ESTREET]  OS=[Unix]  Server=[Samba  2.2.7a]
smb:\> 
```

In this example, `smbclient` connects to the directory share named `tmp` as the Samba user named `chris`. If the password is accepted, you should see information about the server and a `smb:\>` prompt. If you cannot access the same shared directory from a Windows client, it’s quite possible that the client is passing an improper user name and password. Part of the problem may be that the Windows client is not providing encrypted passwords.

For certain Windows clients, using encrypted passwords requires that you change a Windows registry for the machine. One way to change the registry is with the Windows `regedit` command. Registry changes required for different Windows systems are contained within the `/usr/share/doc/samba-*/docs/registry` directory.

> **TIP:** The `smbclient` command, used here to list server information and test passwords, can also be used to browse the shared directory and copy files after you are connected. After you see the `smb:\>` prompt, type `help` to see the available commands. The interface is similar to any ftp client, such as sftp.

## Summary

By providing centralized file servers, an organization can efficiently share information and applications with people within the organization, with customers, or with anyone around the world. Several different technologies are available in Fedora Linux to enable you to make your Fedora Linux computer a file server.

The Network File System (NFS) protocol was one of the first file server technologies available. It is particularly well suited for sharing file systems among Fedora Linux and other UNIX systems. NFS uses standard `mount` and `umount` commands to connect file systems to the directory structures of client computers.

The Samba software package that comes with Fedora Linux contains protocols and utilities for sharing files and printers among Windows and OS/2 operating systems. It uses SMB protocols that are included with all Microsoft Windows systems, and therefore provides a convenient method of sharing resources on LANs containing many Windows systems.

# Chapter 19

# Setting Up a Mail Server

## In This Chapter

- Introducing SMTP and sendmail
- Installing and running sendmail
- Configuring sendmail
- Introducing Postfix
- Stopping spam with SpamAssassin
- Getting mail from the server (IMAP and POP3)
- Configuring SquirrelMail
- Administering a mailman mailing list

Today, electronic messaging is part of the communication backbone, the core of information dissemination within companies of all sizes. Everyone uses e-mail, from the mailroom to the laboratories to the CEO's office. And if you're in charge of an organization's mail server, you'll be notified (incessantly) when it stops working.

This chapter explains how to set up a mail server in Fedora to send and receive messages. In particular, it focuses on configuring a Sendmail mail server, but also tells how to configure a Postfix mail server (which is also in the Fedora Linux distribution). Once the mail server is configured, Fedora provides your mail server's users with different ways of getting their e-mail from your server, such as downloading it to their mail client (with IMAP or POP3) or reading it from a Web browser (using SquirrelMail).

Mailing list configuration and administration (using the mailman software package) are also discussed in this chapter, detailing how mailing list management software integrates and interfaces with the mail server.

> **NOTE:** Although the primary aspects of mail server configuration are discussed in this chapter, many configuration aspects are beyond its scope and thus are not addressed. Because security is an important concern when you're connected to the Internet, it is given considerable focus here.

## Introducing SMTP and sendmail

Even with multimedia attachments and HTML encoding prevalent in e-mail messages today, the technology behind message transfer hasn’t changed significantly since the early 1980s. The framework for the Simple Mail Transfer Protocol (SMTP) was initially described in RFC 821 in 1982. The protocol itself was extended in 1993 (RFC 1425), yielding the Extended Simple Mail Transfer Protocol (ESMTP), which provides more commands and new delivery modes.

The three parts to message transfer are the Mail Transfer Agent (MTA), the Mail Delivery Agent (MDA), and the Mail User Agent (MUA). The MTA, commonly referred to as the mail server (of which sendmail and postfix are examples), actually handles distributing outgoing mail and listening for incoming mail from the Internet. The MDA accepts messages from the MTA and copies the message into a user’s mailbox. Fedora uses procmail as the default MDA, as specified in the sendmail configuration file (`sendmail.conf`). End users, for whom the mail is ultimately intended, use MUAs to get mail from the server and read it from their desktops. Most MUAs support Post Office Protocol (POP3) and Internet Message Access Protocol (IMAP) features for getting mail from the server so it can be read and managed from the user’s desktop computer.

> **CROSS-REFERENCE:** See Chapter 9 for details on Mail User Agents available with Fedora.

This chapter focuses on the sendmail MTA, the most common mail server on the Internet. Nearly 70 percent of all e-mail messages on the Internet are delivered by sendmail. With the growing Internet population, billions of e-mail messages are sent and received each day. As an alternative to sendmail, this chapter also includes a short description of postfix.

For getting mail from the server, this chapter describes the dovecot software package, which includes POP3 and IMAP server software. As an alternative, for allowing users to read and manage e-mail from a Web browser, this chapter describes how to configure SquirrelMail.

There have been three major releases of sendmail. The original sendmail (sendmail version 5) was written in 1983 by Eric Allman, a student at the University of California at Berkeley. He maintained the code until 1987, when Lennart Lövdström enhanced the program and developed IDA sendmail. Eric Allman returned to Berkeley in 1991 and embarked on a major code revision, releasing sendmail V8 in 1993, which incorporated the extensions from IDA sendmail. The current version (8.12.9) is based on this “version 8” code.

## Installing and Running sendmail

In Fedora, the sendmail distribution consists of three RPM packages: sendmail, sendmail-cf, and sendmail-doc. Only the first package is truly necessary to send and receive mail on your machine. The second package includes configuration macros and other files that can help you reconfigure your site’s sendmail installation if the defaults are insufficient. The third package contains documentation files that help to explain some of the details of the current version.

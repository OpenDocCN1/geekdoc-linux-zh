
# CHAPTER 8 | Networked Filesystems and Remote Access

In other words, it uses authentication systems such as the Password Authentication Protocol (PAP), Challenge-Handshake Authentication Protocol (CHAP), and the Extensible Authentication Protocol (EAP). The first two are commonly associated with connections over telephone modem. EAP is an authentication system often used on wireless networks.

Such authentication systems require a username and password database. RADIUS can work with a variety of such databases, including the LDAP, the Network Information Service (NIS), Microsoft's Active Directory, Novell's eDirectory, and even the old standby, the local shadow password suite.

# RADIUS Configuration Files

When installed on an Ubuntu system, configuration options are commented into a number of files in the /etc/freeradis/ directory. On some other systems, you'll find these files in the /etc/raddb/ directory. Table 8-2 describes the function of each of these files and subdirectories.

# Moving Away from Clear-Text Access

To understand the risks associated with clear-text access, take a look at Figure 8-4. It's an excerpt from the Wireshark network analyzer. It can read the contents of every packet sent over the local network. Every system on an Ethernet network can listen in all network communications, even those two remote systems on the LAN. That's the way Ethernet works. Figure 8-3 illustrates the contents of one packet, which happens to be one letter of a password.

Wireshark is readily available for most Linux distributions, including Red Hat and Ubuntu. Early in this chapter, we noted to regular Telnet that can be hiding usernames and passwords in network communication.

![](img/c0608a8c8a0777903dfec4ff61fdffa1_270_0.png)

# The Simple rsync Solution

The rsync command is frequently used for backups. You'll see how backups work in Chapter 14. For now, this section examines the basic features of the rsync command. The first time you back up a system with the rsync command, everything might seem slow. With its archive features, the rsync command can back up more than just the information in regular files. It can preserve more, including the following:

- Ownership by users and groups
- Last file-access times
- Permissions
- Symbolic links between files

An rsync-based backup with all such original information can form the basis for a "gold baseline." The dates associated with files on the backup provide assurance that such files have not been changed after a certain date. Such a date can be important in case of a security breach, especially if your managers suddenly refuse to trust files created after that date.

One of the risks associated with the rsync command is that it normally transmits data in clear text. If SSH clients are installed on the local system, rsync doesn't have to take such risks. For example, the following command takes the contents of user michael's home directory recursively (with all subdirectories) and sends it to the remote system named backup.example in the /backups/ subdirectory:

```
$ rsync -e ssh -ahZ ~michael/backup.example:/backups/
# -e ssh tunnels the backup packets over an SSH connection. If you haven't yet connected to the remote system, the remote SSH server prompts for a password or sends a message to verify the passphrase described earlier in this chapter. The -H transmits hard-linked files in the archive. The -z compresses the data being transmitted, speeding up the backup.
```

# E-Mail Clients

Standard e-mail clients connect to servers using three major protocols: the Simple Mail Transfer Protocol (SMTP), the Post Office Protocol version 3 (POP3), and the Internet Mail Access Protocol version 4 (IMAP4). Most users configure e-mail clients as Evolution, Thunderbird, and specifically Microsoft's Outlook Express to send and receive their e-mail communications using these protocols.

Every time a request to send or receive e-mail is sent from a client to an e-mail server, the username and password is also sent over the network. With those clear-text protocols, it's easy for a black-hat hacker to identify those usernames and passwords with tools such as Wireshark.

# CHAPTER 8 | Networked Filesystems and Remote Access

TABLE 8-3 Clear-text e-mail protocols and secure alternatives.

| CLEAR TEXT E-MAIL PROTOCOL/PORT | SECURE ALTERNATIVE/PORT |
| :--- | :--- |
| IMAP4/143 | IMAPS/993 |
| POP3/110 | POP3S/995 |
| SMTP/25 | SMTPS/465 |

Fortunately, there are secure alternatives to each of those protocols, briefly described in Table 8-3. In these cases, the alternative includes “S” in the name, which is short for secure. In all cases, such protocols communicate over different port numbers. In general, the IMAP4 and POP3 protocols serve e-mail, and the SMTP protocol transmits e-mail from clients.

These are just standard ports. Some e-mail administrators use nonstandard port numbers in the hope that obscurity minimizes attempts by spammers to use their e-mail servers.

Such secure alternatives won’t work unless they’re configured in appropriate e-mail server configuration files. To review how these configuration files work and can be changed, see Chapter 9. Just as few, some e-mail administrators use port 587 for e-mail transmission using the submission protocol, which is for practical purposes interchangeable with port 465 for the secure SMTP (SMTPS) protocol. Some open source SMTP e-mail services can be modified to use either port 465 or 587.

# Best Practices: Networked Filesystems and Remote Access

If you need to set up remote connections by telephone modem, the most popular standard is RADIUS. It can be configured to authenticate users via protocols such as PAP, CHAP, and EAP. It includes a number of complex configuration files stored either in the /etc/radius/ or the /etc/radiusd/.

As you pay attention to cleartext protocols like Telnet, you should also remember the clear-text methods used for backups and e-mail. Fortunately, the advantages of SSH can be incorporated directly into rsync commands. In addition, there are secure versions of major e-mail protocols available that can be configured on client systems. Of course, that still requires a matching configuration on e-mail server systems, one of the topics covered in Chapter 9.

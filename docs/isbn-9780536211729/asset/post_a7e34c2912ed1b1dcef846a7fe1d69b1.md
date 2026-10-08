
## COMMON HACKING BY SUBSYSTEM

In this chapter, common known weaknesses and important configuration techniques of common subsystems will be discussed. You cannot live without some of these services, such as Sendmail and DNS. Others are inherently insecure, and must not be used outside a secure and controlled environment, if security is to be maintained.

The topics covered in this chapter include:

- “NFS, mountd and portmap” on page 120
- “Sendmail” on page 122
- “Telnet” on page 138
- “FTP” on page 138
- “The rsh, rcp, rexec and login Services” on page 146
- “DNS (named, a.k.a. BIND)” on page 149
- “POP and IMAP Servers” on page 152
- “Doing the Samba” on page 156
- “Stop Squid from Inking Out Their Trail” on page 175
- “The syslog Service” on page 178
- “The print Service (lpd)” on page 179
- “The ident Service” on page 179
- “INND and News” on page 180
- “Protecting Your DNS Registration” on page 181

### 3.1 NFS, mountd, and portmap

![](img/7d04225c75a86d3cf4bd6077596f35b2_141_0.png)

NFS stands for Network File System. It allows a client system to “mount” an NFS server system’s remote file systems as if they were directly on the client system. Samba and AppleTalk have more recently created similar facilities. NFS is a powerful capability. Unfortunately, there have been numerous security problems, some of them unsolvable with incompatible protocol changes. Because of this, it is recommended that it not be used at all except on private secure networks, protected from insecure networks, such as the Internet.

Please review “Turn Off mountd, and portmap” on page 92 and “Switch NFS to Run over TCP” on page 93, where many of the problems have been covered in-depth. What are the problems and under what conditions can they be worked around?

- 1. UDP is insecure because it can be spoofed. This can be resolved by protecting the network of NFS systems (servers and clients) from unsecured networks via properly configured firewall and ensuring that only trusted systems running operating systems can attach to the network. This firewall will need to know which IP addresses on interfaces and reject packets received on a different interface than the “real” system with IP address. If the routing system is running Linux (with at least a 2.2 kernel), a firewall is not even necessary as the kernel offers Source Address Verification. This feature enables the kernel to block packets with spoofed source addresses coming from the wrong interface.
- 2. All systems on this network need to be secured against untrustworthy people having root access. This is to prevent crackers who have physical or network access to your Linux and UNIX boxes simply spoofing from an “inside” system. For Windows and Macs, simple password protection is needed, protection against physical access to them by the untrustworthy will increase security. This is due to having a different security model than Linux (Many people have many closed source operating systems to be significantly less than Linux).
- 3. Systems need to be protected against a rogue booting his own operating system off floppy, CD-ROM, or obtaining single-user mode boot disk. This is discussed starting in “Booting the Intruder’s Floppy or CD-ROM” on page 114. Because of NFS’s design, the NFS server will be compromised by the boot process.
- 4. Understand that NFS was created at a time when all computers were big and expensive, only trusted SysAdmins had root access, and systems were kept in locked rooms with very limited access. Anyone with root access can alter her client box to obtain any NFS access offered to any client on the network by a given NFS server. This is done simply by altering the client system’s IP address and using so to gain the privileges of whichever account is offered access by the NFS server.
- 5. Ensure that unprotected systems cannot get packets to your NFS server, mounted portmap (or NFS clients) can be spoofed. This means using IP Chains, preferable on a firewall, or Source Address Verification to block port 2049 (NFS) and port 111 (portmap) for both UDP and TCP from untrusted and unwanted systems.
- 6. Use suitable options when mounting an NFS file system. The most important ones are as follows: The tcp option will cause NFS to use TCP instead of UDP. TCP is much harder to spoof, due to the three-way handshake using random numbers. The nosuid option will allow the Linux kernel to generate any set-UID or set-GID bits on files. The noexec option will prevent the execution of any programs on the file system.
- 7. Use the options available in /etc/exports entries to increase security. In particular, the ro option to make a file system Read/Only that does not need to be writable and the noaccess option to block access to a subtree are helpful. Do not disable root_squash with no_root_squash.

> Even with root_squash, a nonroot user can alter a program that root later invokes, that that will "own" the machine.

Use squash_uids=0-15,20 to squash UIDs 0–15 and 20. This means that if a remote user claims to be UID 1, treat him as he was the nobody account on the server system. This account is presumed to own no files and is allowed only whatever access is granted worldwide. If appropriate, use all_squash to treat all users as nobody. Another possibility is to use map_static=/etc/nfs/nervous.map to use a list that maps remote UIDs into appropriate local UIDs. A typical nervous.map file would look like this:

| #ID | Server | Comments |
| --- | --- | --- |
| uid 0-99 | | # Squash UIDs |
| uid 100-999 | 1000 | # Map 100-999 to 1000-1999 |
| gid 0-99 | | # Squash GIDs |
| gid 100-999 | 1100 | # Map 100-999 to 1100-2099 |

### 3.2 Sendmail

![](img/7d04225c75a86d3cf4bd6077596f35b2_143_0.png)

Almost every Linux shop runs Sendmail and allows any system in the world to connect to it. It needs root to open its privileged port (TCP port 25) and enable all its features. To the kernel, and possibly X, Sendmail may be the most complex component of Linux and you could spend a lifetime learning about it. It will be assumed that your systems have been upgraded to Sendmail 8.10 or higher that you have applied the suggestions that were discussed in "Upgrade sendmail" on page 101 and "Fortify sendmail to Resist DoS Attacks" on page 103. We will proceed from there.

> Although Sendmail 8.9.3 and above are considered secure at present, between that version and 8.10, the configuration file format changed dramatically. Rather than requiring SysAdmins to be an expert on the challenging sendmail.cf for format, this change allows editing the less challenging sendmail.mc file for routine configuration changes. There are other improvements to

If your version of Sendmail is older than 8.9.3, there are known buffer exploits and spam relay exploits that are vulnerable to, so you will want to upgrade immediately. "Upgrade sendmail" on page 101 for the details on upgrading Sendmail. A variety of problems and solutions related to Sendmail will be discussed here. There are other frequent alternatives to Sendmail, such as postfix and gmail. Many people consider these to be easier to use and more secure than Sendmail. Now that Eric Allman, Sendmail's creator, has founded the well-capitalized Sendmail, Inc., there have been good support and new features for Sendmail. The postfix program is recommended by many security experts as a more secure mailer than Sendmail. It was developed by Wietse Venema, one of the most regarded Linux developers, at IBM's TJ Watson Research Laboratory, one of the world's best research labs.

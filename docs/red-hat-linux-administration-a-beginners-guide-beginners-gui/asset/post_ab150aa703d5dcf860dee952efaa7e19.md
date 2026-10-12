
## Module 12: Setting Up Your Web Server Using Apache

1. The server name directive allows you to match the machine name returned by a web server to a CNAME instead of the actual machine name. This can be useful if your machine name does not happen to be www.

2. Apache will start a number of processes and have them wait around for incoming connections. The number of running processes will be increased or decreased according to load.

3. You can include one MPM module on a server.

4. Apache provides modules that allow you to extend Apache’s features.

5. E is the correct answer.

6. HTTP is the Hyperext Transfer Protocol, and it is used to move web pages from the server to your browser.

7. It is stable. Several major web sites, including www.amazon.com and www.generalelectric.com, are using it.
   - The entire program and related components are open source.
   - It works on a large number of platforms (all popular variants of UNIX, some of the not-so-popular variants of UNIX, and even Windows).
   - It is extremely flexible.
   - It has shown itself to be more secure than most of the alternatives.

8. False.

9. True.

10. True.

### Module 11 (Continued from previous page)

11. The anon_world_readable_only default is set to “yes” as a precaution to keep anonymous users from downloading anything that is not explicitly world readable. This is useful if a number of files are owned by the user that vsftpd is running.

12. Setting the configuration option for userlist_enable allows the server to limit who can log in based on a list in a file. It can either allow only those names listed, or can deny those listed.

13. Placing an entry in the /etc/hosts.allow or /etc/hosts.deny files will allow you to explicitly control access to a number of services, including vsftpd.

14. Using passive mode will allow access for clients behind a firewall that doesn’t specially handle FTP connections.

15. Yes. However, each virtual server must have a unique IP address.

16. No. vsftpd must be run from inetd (or xinetd).

## Module 13: Sending Mail with SMTP

1. The SMTP protocol defines the method by which mail is sent from one host to another.

2. B.

3. SMTP is a transport protocol for sending messages only. A user cannot connect to an SMTP server to read his or her mail. POP and IMAP are just the opposite. A client can use POP or IMAP to read mail off of a server, but the client host cannot send e-mail with POP or IMAP.

4. Sendmail now ships the package in a very tight security mode and leaves it to consumers to loosen up only what they wish.

5. IMAP.

6. Mail transfer agent (MTA), mail delivery agent (MDA), and mail user agent (MUA).

7. C.

8. myorigin.

9. Sendmail maintains only one queue, and it is stored in /var/spool/mqueue; spools are stored in /var/spool/mail. Postfix delivers to /var/spool/mail by default; it uses subdirectories under /var/spool/postfix for each of its spools.

10. True.

11. False.

## Module 14: Using POP and IMAP for E-Mail Retrieval

1. The Post Office Protocol (POP) and the Internet Message Access Protocol (IMAP) are protocols for receiving mail from a server for reading.

2. C.

3. E.

4. True.

5. False.

6. True.

7. Basically, IMAP keeps your messages in a mailbox on the server. POP thinks that whatever is on the server is just temporary storage for mail you haven't picked up yet. So when you send your mail through POP, those messages are removed from the server when they're sent to your client. Then IMAP comes in later and sees no messages on the server. (POP already removed them.)

8. The name of the challenge/response mechanism that is available for POP is called Authenticated POP (APOP).

9. The name of the challenge/response mechanism that is available for IMAP is called Challenge-Response Authentication Mechanism (CRAM or CRAM-MD5).

10. Challenge/response mechanisms keep plain text copies of the password database on the server, causing your data to be unprotected there.

## Module 15: The Secure Shell (SSH)

1. If data is encrypted with a public key, it can only be decrypted with the corresponding or private key (or vice versa).

2. SSH is the Secure Shell, and it allows users to connect to a remote server with a session that is 100 percent encrypted.

3. The session will appear much like random garbage going by.

4. True.

5. False.

6. It allows peers to examine the source code and make sure that there aren't any holes that may allow crackers to break the security. The protocols used are in no way weakened by someone viewing how they work.

7. False. Users must also be educated not to compromise security in other ways.

8. It specifies whether sshd should check file modes and ownership of the user's files and home directory. If the permissions are too lax, ssh will deny them login.

9. ssh-keygen.

10. scp or sftp.

## Module 16: Network File System (NFS)

1. Network File System (NFS) is the UNIX way of sharing files and applications across the network.

2. Portmapper is the RPC service manager, and it takes care of telling the client where the actual service is located on the server.

3. Notification to the server is unnecessary because the server does not keep track of all clients that have mounted its file systems.

4. **D.** All of the above.

5. The possible commands are:
   - -a exports all entries in the /etc/exports file.
   - -r re-exports all entries in the /etc/exports file.
   - -u client: /dir/to/mount unexports the directory /dir/to/mount to the host client.
   - -v verbosely prints messages about what it is doing.

6. Possible problems that can occur are:
   - The server can confuse a file with a fully qualified domain name.
   - The server’s perception of the host name/IP pairing is not correct.

7. C. Disables the locking.

8. D. None of the above.

9. False.

10. True.

11. A. Hard.

## Module 17: Network Information Service (NIS)

1. As long as the tabular file has at least one column with a unique value throughout, NIS can use it to share information.

2. The main benefit achieved from using NIS is that you can maintain a central copy of the data; and whenever that data is updated, it automatically propagates to all of the network users.

3. You can query NIS either by listing the entire table or by pulling a specific entry based on a search for a given key.

4. B.

5. True.

6. C.

7. The ypbind daemon is used to find and connect to an NIS server.

8. False. The ypwhich command returns the name of the NIS server that is answering your requests.
   The yppasswd command allows you to change your password entry on the NIS system.

9. When using a netgroup, members are specified in the form host,user,domain.

10. Place at least one NIS server on each end of the WAN connection.

## Module 18: Talking to Windows with Samba

1. Two ways of handling the incompatibility between UNIX and Windows are:
   - Edit the Registry on Windows clients to disable the use of encrypted passwords. The Registry entries that need to be changed are listed in the docs directory in the Samba package.
   - Configure Samba to use Windows-style encrypted passwords.

2. Yes.

3. Samba is a tool for allowing UNIX to share files and printers with Windows-based systems.

4. Samba allows UNIX clients to talk to Windows servers using their native tongue, which means fewer hassles and seamless integration for your users.

5. SMB stands for Session Message Block.

6. Possible answers are **/etc/init.d/smb start** and **/etc/init.d/smb stop**.

7. SWAT is the Samba Web Administration tool; it is a web-based interface for administering Samba.

8. The GlobalS page lists all settings that affect Samba’s operation. These settings are divided into seven groups: Base, Security, Logging, Tuning, Printing, Browse, and WINS.

9. Shares on the SWAT menu are for setting up disk shares and their respective options.

10. The parameter for connecting the **smbclient** to the printer is **-P**.

11. d.

## Module 19: Printing

1. The Internet Printing Protocol.

2. The goal of IPP is to provide a common protocol that can be used across systems, reduce the number of different standards that printers have to support, and cover most printing situations.

3. PostScript is a programming language that is focused on describing text and graphics on a page. This is notable because a PostScript file will appear the same when printed on any printer that supports PostScript.

4. Banner pages show who printed the document and the name of the document. Most sites find that the banner pages are not worth the wasted paper and prefer to keep this feature turned off.

5. The **rm** command specifies the remote print server, and **rp** specifies the printer queue on that server.

6. False. The **/etc/lpd.stats** file shows the stats of the printer.

7. True.

8. The preferred method for setting up the CUPS server is to use a web-based administration interface.

9. An implicit class.

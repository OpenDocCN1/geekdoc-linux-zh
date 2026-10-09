as an alternative to **bmail**, make sure the program is installed on the system, and then add the associated m4 macro to `sendmail.mc` and rebuild `sendmail.cf`.

```
define(`PROCMAIL_MAILER_PATH', '/usr/bin/procmail')dnl
feature(`local_procmail')dnl
MAILER(procmail)dnl
```

More simply, **procmail** can be called by the user using the `.forward` file.

```
"|exec /usr/bin/procmail"
```

In either case, **procmail** configuration is controlled via `/etc/procmailrc` and the `.procmailrc` file in a user's home directory.

# # POP

One of the oldest and best-known solutions to the distributed mail problem is the Post Office Protocol (POP) version 3, defined in RFC 1725. POP clients connect to a POP server, which is the repository for incoming mail. The client downloads the entire contents of the user's inbox to the client machine. The inbox is then processed on the local client. POP works very well for those users who run from a single client over a fast connection. If you operate from a number of clients, then you still have the problem of scattering your inbox folders between machines. A basic POP daemon is included with the AIX base operating system for POP version 3. It is run from `inetd` and can be enabled by simply uncommenting the entry in `/etc/inetd.conf`:

```
# pop3          stream   tcp  nowait  root  /usr/sbin/pop3d pop3d
```

The daemons will serve POP mail for locally defined users. POP uses a password for authentication, although newer implementations make use of Kerberos security services. You shouldn't have any difficulty locating more advanced public domain, shareware, and vendor POP implementations for just about any operating system. This includes both POP3 clients and servers.

# # IMAP

The Internet Message Access Protocol (IMAP), defined in RFC 2060, solves the problem of centralizing the processing of mailboxes accessed from multiple distributed mail clients. The Internet Message Support Protocol (IMSP) extends the IMAP protocol to include administration of address books and clustering multiple IMAP servers. A complete solution requires a friendly IMAP-based user agent that is available for most
# CHAPTER 8 | Networked Filesystems and Remote Access

TABLE 8-3 Clear-text e-mail protocols and secure alternatives.

| CLEAR TEXT E-MAIL PROTOCOL/PORT | SECURE ALTERNATIVE/PORT |
| IMAP4/143 | IMAPS/993 |
| POP3/110 | POP3S/995 |
| SMTP/25 | SMTPS/465 |

Fortunately, there are secure alternatives to each of those protocols, briefly described in Table 8-3. In these cases, the alternative includes “S” in the name, which is short for secure. In all cases, such protocols communicate over different port numbers. In general, the IMAP4 and POP3 protocols serve e-mail, and the SMTP protocol transmits e-mail from clients.

These are just standard ports. Some e-mail administrators use nonstandard port numbers in the hope that obscurity minimizes attempts by spammers to use their e-mail servers.

Such secure alternatives won’t work unless they’re configured in appropriate e-mail server configuration files. To review how these configuration files work and can be changed, see Chapter 9. Just as few, some e-mail administrators use port 587 for e-mail transmission using the submission protocol, which is for practical purposes interchangeable with port465 for the secure SMTP (SMTPS) protocol. Some open source SMTP e-mail services can be modified to use either port 465 or 587.

# Best Practices: Networked Filesystems and Remote Access

While it’s best to minimize the number of networked services on any one system, that may not be enough for a security system. Ideally, all you on a server is one networked service and an SSH server to administer that remote service. But if you need Kerberos authentication, you’ll need a Kerberos server as well. And keeping Kerberos servers in sync requires if you use Kerberos servers, stick with version 5. Once these are configured, you’ll note that those clients that connect to your servers have been previously authenticated with genuine Kerberos tickets.

One benefit of Kerberos is with services such as NFS. While NFSv4 doesn’t authenticate by user, it can help to authenticate NFSv4 clients with Kerberos. Shared NFS directories that look for Kerberos tickets are less likely to fall into the hands of black-hat hackers.

The vsFTP service can be secured in a number of ways with respect to special directories, privilege management, timeouts, user lists, and more. Most vsFTP options are configured in the vsftpd.conf file, users can be limited in the ftpusers and user_list files. When enabled, PAM can further enhance vsFTP security.
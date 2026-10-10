reader does this, SSH kicks in and forwards traffic to the SSH server, which then passes the data on to the local port 143, which is presumablly running the real IMAP server. All of this is hidden from the e-mail reader program; as far as it's concerned, it's retrieving e-mail from a local IMAP server.

# SSH Security Considerations

SSH is intended to solve security problems rather than create them. Indeed, on the whole using SSH is superior to using Telnet for remote logins, and SSH can also take over FTP-like functions and tunnel other protocols. Thus, SSH is a big security plus compared to using less-secure tools.

Like all servers, though, SSH can be a security liability if it's run unnecessarily or inappropriately. Ideally, you should configure SSH to accept only protocol level 2 connections and to refuse direct *root* logins. If X forwarding is unnecessary, you should disable this feature. If possible, use TCP Wrappers or a firewall to limit the machines that can contact an SSH server. As with all servers, you should keep SSH up to date; there's always the possibility of a bug causing problems.

You should consider whether you really need a remote text-mode login server. Such a server can be a great convenience—often enough to justify the modest risk involved. For extremely high-security systems, though, using the computer exclusively from the console may be an appropriate approach to security.

One unusual security issue with SSH is its keys. As noted earlier, the private-key files are extremely sensitive and should be protected from prying eyes. Remember to protect the backups of these files, as well—don't leave a system backup tape lying around where it can be easily stolen.

# Using GPG

SSH is designed to encrypt interactive login sessions and file transfers. Sometimes, though, another type of encryption is desirable: You may want to encrypt e-mail messages or files sent to another person via some other means. E-mail was never designed as a secure data transfer tool, and most e-mail messages pass through several e-mail servers and network routers. A compromise at any one of these points enables a cracker to sniff e-mail traffic and extract sensitive data, such as credit card or Social Security numbers. Encrypting your e-mail keeps such details private.

The usual tool for encrypting e-mail is the GNU Privacy Guard (GPG or GnuPG; http://www.gnupg.org) package. This package is an open source re-implementation of the proprietary Prettty Good Privacy (PGP). In addition to encrypting messages, GPG enables you to digitally "sign" messages. Used in this way, messages can be read by recipients who lack the GPG software or appropriate keys; but those who have these tools can verify that the contents haven't been tampered with.
![](bbox=[0.17, 0.22, 0.26, 0.3])

> The use of inetd eliminates the need for a "master" telnetd process running as root, which is a situation that could be particularly dangerous if a security vulnerability were to be uncovered in telnetd. Many daemons (among them sshd, httpd (Apache), and sendmail) do run in this "stand-alone" mode rather than being called out of inetd. The master process (running as root) listens for the new connections and spawns new processes, owned by an unprivileged user, to handle each transaction. This allows for greater flexibility and speed in the program at the expense of a centralized security risk. inetd also runs as root, so it is just as dangerous if it is compromised. The more daemons that run as root, the more possibilities there are for security holes to be found.

Examining the /etc/inetd.conf file shows us that nearly all entries in it are disabled in the out-of-the-box configuration, assuming that you've selected the default security settings during setup. The only ones that are enabled are listed in Table 7.2.

# TABLE 7.2 System Services Controlled by inetd That Are Enabled by Default

| Service | Description | Port(s)/Resources Used |
|---|---|---|
| ftp | File Transfer Protocol | Port 21/TCP |
| telnet | Remote terminal | Port 23/TCP |
| comsat | "biff" server (notifies users of incoming mail) | Port 512/UDP |
| ntalk | command-line chat server | Port 518/TCP;UDP |
| ftp (IPv6) | File Transfer Protocol | IPv6 |
| telnet (IPv6) | Remote terminal | IPv6 |

Other services that you might want to enable, depending on what you're using your system for, are shown in Table 7.3.

# TABLE 7.3 Other Useful inetd Services

| Service | Description | Port(s)/Resources Used |
|---|---|---|
| pop3 | Post Office Protocol | Port 110/TCP |
| imap4 | Interim Mail Access Protocol (server-side mail) | Port 143/TCP |
| smtp | Qmail (alternative to Sendmail SMTP server) | Port 25/TCP |
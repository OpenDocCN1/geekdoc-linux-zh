# 3.11 The print Service (lpd)

Do not use syslogd -r unless you really need it and ensure that the firewall blocks access to UDP port 514. The nsyslog program is a replacement for syslog that offers SSL-wrapped TCP connection for security. It may be downloaded from

```
http://coombs.anu.edu.au/~avalon/nyslog.html
```

# 3.11 The print Service (lpd)

![](bbox=[0.068, 0.303, 0.933, 0.355])

The standard Linux lpd program listens on TCP port 515 for remote print job requests. Its security is patterned on the flawed R* security found in rsh and its brethren are discussed in "The rsh, rcp, rexec, and login Services" on page 146. The lpd will accept jobs from systems and users specified in /etc/hosts.equiv and /etc/hosts.allow. It is strongly recommended that the firewall block this port to all untrusted systems. A weaker alternative is to edit /etc/services or invoke lpd with an alternate port number that crackers are less likely to detect and attack.

The port number is specified on the command line as a simple number (with no dash) when lpd is started. If network access is possible (local or remote), it is suggested to start lpd with the -f flag to cause logging of requests via syslogd. The danger level has been boosted for the second edition because of a huge number of compromises in early 2001 due to a Red Hat bug and crackers continuing to attack this port frequently.

# 3.12 The ident Service

![](bbox=[0.068, 0.713, 0.933, 0.765])

The ident service operates via the ident program that can either operate as a daemon or being started by inetd. When someone uses a client program, such as Netscape, telnet, or FTP from your system connects to a server on a remote system, that remote system is told only your system's IP address and what port number on it initiated the connection. There is no way for the ident system to know what user from your system has connected to it or even if they have spoofed your IP address. If there is mischief caused by one of your users, that remote system cannot identify which user caused it and report the user to you. The ident service offers answers to these questions by telling the
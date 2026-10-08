
Various ports in this range are used by Trojan hackers that a cracker will install on a compromised system. Do you really want the next DDoS attack that makes national news to be traced to your system?

My suggestion would be to start with

```
acl Safe_ports port 80 21 443 563 70 210
http_access deny !Safe_ports
```

and allows you to present a case for allowing any other ports. See the CD-ROM for a list of the most popular default cracker ports, as encoded in the ports program source.

## 3.10 The syslog Service

![](img/7d04225c75a86d3cf4bd6077596f35b2_199_0.png)

The syslog facility is used by many of the daemons and the kernel to log error messages and advisory messages. It has a facility to accept messages from remote systems over UDP port 514. This is a convenient way to consolidate messages from multiple systems and then just scan and review one log file. Recent versions of syslog require the -r flag to enable it to listen on UDP port 514 for messages from remote systems to be logged. This is a welcome security enhancement that allows the large majority of systems that do not make use of this feature to be immune from crackers sending to this port.

The remote logging feature can increase security by logging activity on a system remotely. Thus, if a system is compromised and all log files destroyed, you still have the data on the remote system, assuming that the remote system is not also compromised. By having a special "high-security" system with minimal services supported (to reduce the likelihood of compromise) handle the logging, the chance of all logs being destroyed is minimized. This is discussed in "Monitoring Your System" on page 343.

However, UDP packet spoofing is true. Fortunately, modern versions of syslog (v1.3, as noted as far back as Hat 6.0) do not monitor UDP port unless configured to do so. There have been some exploits that can cause a DoS by repeatedly sending packets to syslog and deny access to legitimate clients or to fill up space due to the volume of logged messages. Occasionally, a cracker will write fake log messages to various systems that have this port accessible from the Internet.

There may be ways to gain root access, though hopefully these have been fixed by the time you read this, assuming that you have the latest syslog. Certainly, some crackers will spoof their UDP source IP, which is trivial, and then send messages. These will be logged and certainly confuse you. They may falsely indicate a break-in by any text they may have placed in them.

The clear solution is to have your firewall block this port from access by sites outside the trusted network.

Do not use syslogd -r unless you really need it and ensure that the firewall blocks access to UDP port 514. The nsyslog program is a replacement for syslog that offers SSL-wrapped TCP connection for security. It may be downloaded from

```
http://coombs.anu.edu.au/~avalon/nyslog.html
```

## 3.11 The print Service (lpd)

![](img/7d04225c75a86d3cf4bd6077596f35b2_200_0.png)

The standard Linux lpd program listens on TCP port 515 for remote print job requests. Its security is patterned on the flawed R* security found in rsh and its brethren, which is discussed in "The rsh, rcp, rexec, and login Services" on page 146. The lpd will accept jobs from systems and users specified in /etc/hosts.equiv and /etc/hosts.allow. It is strongly recommended that the firewall block this port to all untrusted systems. A weaker alternative is to edit /etc/services or invoke lpd with an alternate port number that crackers are less likely to detect and attack.

The port number is specified on the command line as a simple number (with no dash) when lpd is started. If network access is possible (local or remote), it is suggested to start lpd with the -f flag to cause logging of requests via syslogd. The danger level has been boosted for the second edition because of a huge number of compromises in early 2001 due to a Red Hat bug and crackers continuing to attack this port frequently.

## 3.12 The ident Service

![](img/7d04225c75a86d3cf4bd6077596f35b2_200_1.png)

The ident service operates via the ident program that can either operate as a daemon or be started by inetd. When someone uses a client program, such as Netscape, telnet, or FTP from your system to connect to a server on a remote system, that remote system is told only your system's IP address and what port number on it initiated the connection. There is no way for the ident system to know what user from your system has connected to it or even if they have spoofed your IP address. If there is mischief caused by one of your users, that remote system cannot identify which user caused it and report the user to you. The ident service offers answers to these questions by telling the remote system which of your users has this port number. The identd server can also be configured to log these queries for later analysis.

The ident service gives information about your system to any process that asks. If allowed to give out user names, these might be used by an attacker to guess passwords or e-mail addresses. Recall that a valid user name and that user's password must be supplied for any information to be discerned from a login attempt. It is suggested that the -n flag be given when identd is invoked to cause a numeric UID to be given instead of a user name because the UID is of no use for this purpose. Also, it is suggested that the -user and -group flags be used to change ident to change itself to a harmless user and group, such as ident. Thus, in case a cracker finds a vulnerability in it, the cracker will not get access.

> You might want to modify identd to provide the same response (the fake user name) each time it is queried. This will prevent crackers from finding who is logged on, and will prevent both crackers and spammers from getting user names for nefarious purposes. You can download such a fake version from www.ajk.tele.fi/~too/sw/

Additionally, DoS attacks are possible, because it is a resource that an attacker can use up. It is suggested that if it is run, be run only on systems that have "real users" with shell accounts. (Other systems have no use for it.) The -o option, which is off by default, will cause identd to say that the operating system is OTHER instead of UNIX. While some people advocate for "security by obscurity," I do not find such a technique particularly valuable, though I do not believe in revealing user numbers; that information would accurately reveal vulnerabilities.

The -l option will cause identd to log requests via syslog. It is on by default.
A decent cracker can determine your system's operating system by observing differences in how it responds to certain conditions in packet handling. The nmap program is particularly skilled at doing this. Even this will not be necessary if you supply such information via a telnet service or the offering of other services characteristic of Linux and UNIX. If in doubt, do not offer identd.

## 3.13 INND and News

| DANGER LEVEL |
| :--- |
| 💀💀💀 |

These servers provide Usenet (Network) News, also known as "The News Groups," or News. On many recent distributions, INND is enabled by default. It uses a fair amount of resources when enabled and even in the default configuration, it uses cycles. Certainly, unless you will be using it, it should be turned off, as should any unneeded service.

Other than being resource-intensive if a large number of groups are processed, these services seem to be relatively safe. They should run as the news user and group. Forged postings should be expected and thus sender information is not to be trusted. INND and News use the nntp port (Network News Transfer Protocol port), TCP port 119. To disable, you should issue the command

```
/etc/rc.d/init.innd stop
chkconfig innd off
```

## 3.14 Protecting Your DNS Registration

DANGER LEVEL

This is an area of security that never occurs to most Sysadmins to worry about. Simply, they register with the helpful folks at Network Solutions and never worry about their multi-million dollar company riding on about 80 bytes of data that map their domain name to the IP address of the name servers. See "AOL's DNS Change Fiasco" on page 558 for the "really big" problem that faced AOL. Sometimes, you may want to change this information, particularly when changing ISPs or when changing systems that act as name servers. Certainly, remembering passwords is a bother, and you risk losing them.

Network Solutions provides three ways to change this information electronically. The default way is to send email from an account listed as that of the registrant or technical contact. As everyone knows now, it is trivial to spoof these. This is what happened to AOL and can happen to the vast majority of domain owners who are set up for this method. The solution is to change your domain's authentication method by which you connect to Network Solutions.

The two other methods are by the use of a password or by the use of a PGP key. In the password method you supply a, um, ah, password. Network Solutions calls this CRYPT-PW method. Using this method, Network Solutions encrypts your supplied password and stores it similarly to how Linux stores the encrypted versions of users' passwords. To change information, you will need to supply the original password. Even if a cracker compromises Network Solutions (though I have not heard of this happening), the cracker cannot obtain your password.

A minor weakness in this scheme is that the encryption algorithm seems to pass the first two characters of the unencrypted password without change. Thus, it is suggested that the first two characters not be of an easily guessed word. This is a minor problem because the encrypted password is not public information. Use a good password, as discussed in "Avoiding Weak and Default Passwords" on page 36.

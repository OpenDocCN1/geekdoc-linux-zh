
# Nmap: network port scanner

From the example, we can see that the host ubuntu is running two services that are likely to be unused and that have historically associated with security problems: portmap (rpcbind) and an email server (smtp). An attacker would likely probe those ports for more information as a next step in the information-gathering process.

The STATE column in nmap's output shows open for ports that have listening, closed for ports with no server, unfiltered for ports in an unknown state, and filtered for ports that cannot be probed as unfiltered unless an attacker is running an ACK scan. Nmap does not classify ports unless it is running a more secure server, secure.booklab.atrust.

```
ubuntu$ nmap -ST secure.booklab.atrust
```

Nmap 4.20 (http://nsecure.org ) at 2009-11-01 12:42 MST
Interesting ports on secure.booklab.atrust (192.168.20:35):
Not shown: 1691 closed ports

| PORT | STATE | VERSION |
| :--- | :--- | :--- |
| 25/tcp | open | smtp Postfix smtpd |
| 80/tcp | open | http lightd 14.13 |

Nmap finished: 1 IP address (1 host scanned) in 0.143 seconds

In this case, it is clear that the host is set up to allow SMTP (email) and an HTTP server. A firewall blocks access to other ports.

In addition to straightforward TCP and UDP probes, nmap also has a repertoire of sneaky ways to probe ports without initiating a connection. In some cases, nmap probes with packets that look like come from the middle of a TCP conversation (rather than the beginning) and waits for 답 packets to be sent back. These stealth probes may be effective at getting past a firewall or avoiding detection by a network security monitor on the lookout for port scanners. If your site uses a firewall (see Firewalls on page 932), it's a good idea to probe it with these alternative scanning methods to see what they turn out.

nmap has the magical and useful ability to guess what operating system is running by looking at the particulars of its identification of TCP/IP. It can sometimes identify the software that's running on an open port. The -O and -sV options, respectively, turn on this behavior. For example:

```
ubuntu sudo nmap -sV -O secure.booklab.atrust
```

Starting Nmap 4.20 (http://nsecure.org ) at 2009-11-01 12:44 MST
Interesting ports on secure.booklab.atrust (192.168.20:35):
Not shown: 1691 closed ports

| PORT | STATE | VERSION |
| :--- | :--- | :--- |
| 25/tcp | open | smtp Postfix smtpd |
| 80/tcp | open | http lightd 14.13 |

Device type: general purpose
Running: Linux 2.4.X[2.5.X]2.6.X
OS details: Linux 2.6.16 - 2.64

Nmap finished: 1 IP address (1 host scanned) in 8.095 seconds

![](img/579efec8c67772f31ecf34844bbb71a2_963_0.png)

# Chapter 22 Security

This feature can be very useful for taking an inventory of a local network. Unfortunately, it is also very useful to hackers, who can base their attacks on known weaknesses of the target OSES and servers.

Keep in mind that most administrators don't appreciate your efforts to scan their network and point out its vulnerabilities, however intended your motive. Do not run nmap on someone else's network without permission from one of that network's administrators.

# Nessus: next-generation network scanner

Nessus, originally released by Renaud Daiseran in 1998, is a powerful and useful vulnerability scanner. At this point, it uses more than 31,000 plug-ins to check for both local and remote security flaws. Although it is now a closed source, proprietary product, it is still freely available, and new plug-ins are released regularly. It is the most widely accepted and complete vulnerability scanner.

Nessus prides itself on being the security scanner that takes nothing for granted. Instead of assuming that all web servers run on port 80, for instance, scans for web servers running on any port and checks them for vulnerabilities. Instead of relying on the version numbers reported by the service it has connected to, Nessus attempts to exploit known vulnerabilities to see if the service is susceptible.

Although a substantial amount of setup time is required to get Nessus running (it requires several packages that are not installed on a typical system), it's worth the effort. The Nessus system includes a client and a server. The server acts as a database and the client handle the GUI presentation. Nessus scanners and clients exist for both Windows and UNIX platforms.

One of the greatest advantages of Nessus is the system's modular design, which makes it easy for third parties to add new security checks. Thanks to an active user community, Nessus is likely to be a useful tool for years to come.

# John the Ripper: finder of insecure passwords

One way to thwart poor choices is to break the passwords yourself and force users to change passwords that you have broken. John the Ripper is a sophisticated tool by Solar Designer that implements various password-cracking algorithms in a single tool. It replaces the tool crack, which was covered in previous editions of this book.

Even though most systems use a shadow password file to hide encrypted passwords from public view, it's still wise to verify that your users' passwords are crack resistant. Knowing a user's password can be useful because people tend to use the same password over and over again. A single password might access to another system, decrypt files stored in a user's home directory, and allow access to

- 5. Especially the passwords of system administrators who have sudo

financial accounts on the web. (Needless to say, it's not very security-smart to re-use a password this way. But nobody wants to remember them passwords.)

Considering its internal complexity, John the Ripper is an extremely program to use. Direct john to the file to be cracked, most often /etc/shadow, and watch the magic pattern:

```
$ sudo /john /etc/shadow
Loaded 25 passwords with 25 different salts (FreeBSD MD5 [32/22])
password (jsmith)
badpass (tjones)
```

In this example, 25 unique passwords were read from the shadow file. Passwords are cracked, John prints them to the screen and saves them to a file john.pot. The output contains the password in the left column with the login in parentheses in the right column. To reprint passwords after John has completed, run the command with the -show argument.

As of this writing, the most recent version of John the Ripper is 1.7.3.4. It is available from openwall.com/john. Since John the Ripper's output contains the passwords it has broken, you should carefully protect the output and delete it as soon as you are done checking to see which users' passwords are insecure.

As with most security monitoring techniques, it is important to obtain explicit management approval before cracking access with John the Ripper.

# hosts_access: host access control

Network firewalls are a first line of defense against access by unauthorized hosts, but they shouldn't be the only barrier in place. Two files, /etc/hosts.allow and /etc/hosts.deny, also referred to as TCP wrappers, can restrict access to services according to the origin of network requests. The hosts.allow lists hosts that are allowed to connect to a specific service, and the hosts.deny file restricts. However, these files control access only for services that are hosts_access aware, as those managed by xinetd, sshd, and some.

The format of an entry in either file is *service: host* or *service: network*. Failed connection attempts are noted in syslog. Connections from hosts that are not permitted to access the service are immediately closed. Most Linux distributions include `hosts.allow` and `hosts.deny` files by default, which are usually empty. Our other systems all TCP wrappers as an option after installation. We suggest denying access by default and permit access only to essential services from

```
sshd: 192.168.0.0/255.255.0.0
sendmail: ALL
```

![](img/579efec8c67772f31ecf34844bbb71a2_965_0.png)

# Chapter 22 Security

The format of an entry in either file is *service: host* or *service: network*. Failed connection attempts are noted in syslog. Connections from hosts that are not permitted to access the service are immediately closed. Most Linux distributions include `hosts.allow` and `hosts.deny` files by default, which are usually empty. Our other systems all TCP wrappers as an option after installation. We suggest denying access by default and permit access only to essential services from

```
sshd: 192.168.0.0/255.255.0.0
sendmail: ALL
```

# Bro: the programmable network detection system

Bro is an open source network detection system (NIDS) that monitors network traffic and looks for suspicious activity. It was originally written by Vern Paxson and is available from bro-ids.org.

Unlike NIDSs, Bro monitors traffic flows rather than just matching patterns inside packets. This method of operation means that Bro can detect suspicious activity based on who talks to whom, without matching any string or pattern. For example, Bro can

- Detect systems used as "stepping stones" by correlating inbound and outbound traffic
- Detect a server that has a back door installed by watching for unexpected connections immediately after an inbound
- Report corrected passwords (ignore the incorrect guesses)

Snort (snort.org) is an open source network intrusion prevention and detection system originally written by Marty Roesch and now maintained by Sourcefire, a
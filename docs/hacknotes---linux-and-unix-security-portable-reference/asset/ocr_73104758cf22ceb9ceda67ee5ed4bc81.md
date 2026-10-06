# Software Vulnerabilities BIND (Berkeley Internet Name Domain) is the most widely used DNS server on the Internet. The next paragraph documents a well-known BIND vulnerability.

+   - BIND NXT Overflow and DOS Vulnerabilities This vulnerability was caused by BIND's failure in processing input validation of NXT records. It is possible to remotely exploit this by forcing a vulnerable DNS server to fetch a meticulously crafted NXT record. Other DOS (Denial Of Service) vulnerabilities were also announced in the BIND advisory located at http://online.securityfocus.com/bid/788.

Consider using djbdns as a replacement for BIND. The djbdns program is available at http://cr.yp.to/djbdns.html.

# TFTP (Trivial File Transfer Protocol): 69 (UDP)

TFTP is a UDP-based protocol used to transfer files. It lacks most features as authentication and directory listing. TFTP only supports reading and writing files from and to a remote server.

Sniffing Since TFTP is a clear-text protocol, it is possible to sniff the data being transferred.

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
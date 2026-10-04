
issue the query to these servers; it is up to the server to answer or to delegate authority to another server.

## Domain and IP Registars

To become an authoritative server, you must host and register a domain and/or IP address with an authorized registrar. Initial top-level domains were first approved in 1995. Since 1995, general end users can be registered with general registrars. You can easily find an unofficial listing of general domain registrars by searching the word "registrar" on any major search engine.

Specific TLD extensions were reserved for organizational purposes. Currently .mil and .gov strictly enforced this policy. With correct approval, .mil .gov domains can be registered through government registrars (www.nic.mil and www.nic.gov, respectively). End users (also known as second-level domains) can be purchased through their specific appropriate registrars. Depending on the purpose of the domain, many registrar options are available.

When domains are registered, registrars keep contact information on file. You can see the contact information for the synergy domain by searching at www.networksolutions.com/cgi-bin/whois/whois, as Figure 8.7 shows. The information contained in the registrar database is commonly the best contact method for abuse or direct technical contact.

Figure 8.7 Registrar WHOIS

![](img/729efc56f204a2ebffb8295c3a2dfdfb_439_0.png)

www.synergy.com

Chapter 8 · Attacking and Defending DNS

IP registrars are distributed in a hierarchical method similar to names themselves. Internet Assigned Numbers Authority (IANA) is the main controller of IP addresses, however, RIRs delegate authority to four Regional Internet Registries (RIRs). RIRs control IP records based on worldwide regional area.

Table 8.6 shows the registries of specific regions. Successful lookups must be done through the appropriate RIR WHOIS database (see Figure 8.8) that controls the searched IP block. Common command-line tools, such as towhm by Mark Burnett (www.xato.net/Downloads/towhm.zip), can reverse lookups easily quicker.

## Table 8.6 Designated RIRs

| RIR | Designated Registry | Web Site | Authoritative Region |
| --- | --- | --- | --- |
| ARIN | American Registry for Internet Numbers | www.arin.net | United States, partial control of Africa |
| RIPE | Réseaux IP Europens | www.ripe.net | Europe, Middle East, partial control of Africa |
| APNIC | Asia Pacific Network Information Centre | www.apnic.net | Asia/Pacific Rim |
| LACNIC | Latin American and Caribbean IP Address Regional Registry | http://lacnic.net | Latin America |

## Figure 8.8 Regional RIR WHOIS Output

![](img/729efc56f204a2ebffb8295c3a2dfdfb_440_0.png)

www.synergy.com

## Tools & Traps...

## Using the Bogons List

A maintained listing of IP addresses that are not currently in use or should never be seen on the public Internet is available at www.cymru.com/Documents/bogon-list.html. This list is known as the Bogons List. Since the creation of the Bogons List by Rob Thomas, it has become good practice to block these IP addresses at network borders and within applications because they can be used for illegitimate traffic.

Remember to keep up to date with this list because new IP blocks are changed or reassigned regularly.

## Exploiting DNS

Depending on the skill level of an attacker, exploiting DNS can be trivial (see Table 8.7). Advanced vulnerabilities such as cache poisoning, DoS, and buffer overflows can manipulate server response, or even compromise an entire system. Simplistic vulnerabilities, zone transfers, and version lookups, however, are only information disclosure risks and usually do not breach DNS security.

## Table 8.7 Common DNS Attacks

| Name | Vulnerabilities | Vulnerability Rating | Attack Method |
|---|---|---|---|
| Zone transfer | Information disclosure of hosted domain names | Low | Performing an unrestricted zone transfer, or for forge appropriate approval. |
| Version lookups | Disclosure of software version | Low | Performing lookup of version file to aid future exploitation. |
| DoS | Overworking a system's limited resources, leading to system or service inaccessibility | Medium | Sending or requesting more resources than available. |

## Table 8.7 Common DNS Attacks

| Name | Vulnerabilities | Rating | Attack Method |
| :--- | :--- | :--- | :--- |
| Cache poisoning | Process of injection forged data into the cache of the DNS server | Medium-high | Performing a lookup on an attacker's DNS server. Attackers reply contains additional injected information. |
| Buffer overflow | Sending specific data that overflows a variable and allows memory execution | High | Sending specially crafted packets can overflow buffers and cause a complete daemon crash. |

## Zone Transfers

When a single server is not sufficient to handle a DNS load, multiple servers can be deployed. Zone transfers were invented because it is important for data on all servers to be identical. Zone transfers are a proprietary type of data sharing capability in DNS. A server downloads all information about a specific zone from another server and saves it locally. Transfer access is not always limited, however, even though they are bad administrative practice, public zone transfers are common.

When a DNS server mirrors a primary DNS server's data, it initiates a transfer. A slave server issues a zone transfer and downloads records from master server. Depending on how zone transfers are restricted, results can vary. A successful zone transfer will display all zones and the respective records. Records that include names as *vpn* or *mss* can help an attacker specify targets and internal addresses.

```
ambient@specs~# <<< DiG 9.1.3 @ns1.example.com example.net axfr
;; global options: printcmd
example.net. IN SOA
example.net.root.example.net. 102130 3600 1000 360000 86400
example.net. IN NS
```

Attacking and Defending DNS • Chapter 8

example.net. IN MX mail.example.net.
example.net. IN A 192.0.34.166
example.net. IN A 192.0.34.166
example.net. IN SOA
example.net. 102130 3600 1000 360000 86400
;; Query time: 3 msec
;; SERVER: 192.0.34.166 #53 (ns1.example.com)
;; WHEN: Sun Nov 24 01:01:01 2002
;; XFR size: 8 records
ambient@specops]#

If zone transfers are not possible, underground tunnels are available to brute force DNS. Common hosts are vpn or intranet cannot be guessed. Depending on the goals of attacker, proprietary information can almost always be discovered in DNS.

## Version Discovery

Discovering software vulnerabilities helps attackers profile a server. Version lookups are commonly overlooked information disclosure vulnerabilities. Even with a security viewpoint, versions give an invitation to a hacker. Software information is rarely needed and Berkeley Internet Name Domain (BIND) responds to many dig queries and allows remote attackers to identify their version. The following is a server running BIND; the version and daemon disclosure:

```
root@specialops]# dig @ns1.example.com version.bind CHAOS txt
```

```
DIG 9.1 @ns1.example.com version.bind CHAOS txt
;; global options: printcmd
;; Got answer:
;;HEADER opcode: QUERY, status: NOERROR, id: 40007
;; flags: qr rd; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_443_0.png)

Chapter 8 • Attacking and Defending DNS

```
; QUESTION SECTION:
version.bind.          CH      TXT
```

```
; ANSWER SECTION:
version.bind.      0  CH      TXT      "9.1.3"
```

```
; Query time: 22 msec
; SERVER: 127.0.0.1#53 (ns1.example.com)
;; WHEN: Wed Nov 24 01:01:02 2002
; MSG SIZE rcvd: 48
```

Depending on the DNS server, version files' syntax can be named differently. A universal filename is chaos.txt or version.txt, though the version.daemon syntax is prevalent.

## DoS Attacks

DNS servers are susceptible to DoS attacks, and freely available tools can make DoS an easy option by an attacker. Flooding a DNS server with spoofed SYN packets can fill a system's limited TCP ports, preventing communication to the server via TCP. Brute force DoS of bandwidth resources can fill upstream access and halt communication by clients. Network-intensive DoS attacks can use up network resources.

Spoofed source DoS (DDoS) attacks are by far the hardest DoS attack to protect against; servers under DDoS have been reported to receive upwards of 1 million packets per second. Attacks of this magnitude can cri any server even in the most strategic network locations. Alan Paller, SANS Institute Research Director, states, "Only the richest companies can defend themselves against this type of attack, and most of them can stand a concerted attack".

## Cache Poisoning

In November 2000, Infosec (www.info-sec.com) asserted that one in three organizations with an Internet presence were vulnerable to DNS poisoning. The capability to alter DNS responses the entire DNS chain of authority, therefore making DNS untrustworthy. Cache poisoning was, and is, popular with IRC hackers; having decreased, many servers are still vulnerable and cache poisoning is still a possible exploit.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_444_0.png)

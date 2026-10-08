
# Hacking Exposed Web Applications

![](img/2c61c2d28445b774d9266972920f432d_54_0.png)

Figure 2-1. Running a query at ARIN elucidates IP addresses registered to an organization.

| Whois Server | Addresses |
| :--- | :--- |
| European IP Address Allocation | http://www.ripe.net/ |
| Asia Pacific IP Address Allocation | http://www.apnic.net |
| U.S. military | http://www.nic.mil |
| U.S. government | http://www.nic.gov |

Table 2-1. U.S. Government, Epoch, and Non-U.S. Internet Address Registries

# Chapter 2: Profiling

we’ve used require -h hostname. The following example shows a Windows whomis client (note the use of the "victim" syntax, the trailing dot as a wildcard):

```
C:\whois -h whois.csnic.net victim.
```

Whois Server Version 1.3

Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

```
VICTIMVU.ORG
VICTIMVU.NET
VICTIMVU.COM
VICTIMUK.ORG
VICTIMUK.NET
VICTIMUK.COM
VICTIMSU.ORG
VICTIMSU.NET
VICTIMSU.COM
VICTIMSICKS.ORG
[etc].
```

To single out one record, look it up with "xxx", where xxx is one of the records displayed above. If the records are the same, look them up with "=xxx" to receive a full display for each record.

We can perform further queries on each of the domains listed within this output to obtain the registrar for each domain, as shown (note that here we are querying for the full "victim.com" domain):

```
C:\whois -h whois.csnic.net victim.com
```

Whois Server Version 1.3

Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

```
Domain Name: VICTIM.COM
Registrar: REGISTER.COM, INC.
```

# Hacking Exposed Web Applications

```
Whois Server: whois.register.com
Referral URL: http://www.register.com
Name Server: NS1.VICTIM.COM
Name Server: NS2.VICTIM.COM
Updated Date: 07-feb-2002
```

Once we've identified the registrar (in this example, Register.com, Inc.), we can then perform an organizational query using that registrar's server, as shown below (note that here we only specify the target organization name, "victim").

```
C:\>whois -h whois.register.com victim
```

Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

```
VICTIM.ORG
VICTIM.NET
VICTIM.COM
```

If an organizational query against a specific registrar's whois server turns up no matches, try one of the more comprehensive whois servers such as rs.internic.net or whois.crnic.net, and/or use the dot as wildcard. For example, you could perform an organizational query against rs.internic.net using victim.., as shown below:

```
C:\>whois -h rs.internic.net victim.
```

Whois Server Version 1.3

Domain names in the .com, .net, and .org domains can now be registered with many different competing registrars. Go to http://www.internic.net for detailed information.

```
Aborting search 50 records found ....
VICTIM-AIR.NET
VICTIM-AIR.COM
VICTIM-AH.COM
VICTIM-AGRO.COM
VICTIM-AGRI.COM
VICTIM-AGREE.COM
VICTIM-AGENCIES.COM
VICTIM-AGE.COM
VICTIM-AG.NET
```

# Chapter 2: Profiling

VICTIM-AG.COM

VICTIM-AFRICA.NET
VICTIM-AFRICA.COM
VICTIM-AERO.COM
[etc.]

The main limitation to whose organizational queries against a typical server is that they limit the number of records that will be returned (note that this query was curtailed after 50 records). If the target organization has more than 50 domains, this is a severe limitation. Organizations wishing to receive unrestricted information can typically e-mail the appropriate registrar via the organizational administrative point-of-contact and resort to a series of queries. Otherwise, you'll have to trickery: appending an incremented value and a dot to series of queries. If you want to find all domain names registered to a company name Victim, you could perform a query using victim1, victim2, victim3, and so on—you've exhausted the most typical possibilities for registered domain names. Tedious, but if your goal is comprehensiveness, you have few other choices via whomis.

One of our favourite tools is Sam Spade, which is available as a Win32 client, or you can turn to http://www.samspade.org and use the Web-based tools from any Internet-connected browser.

# DNS Interrogation

You have noted that whomis queries turned up the identity of the DNS name servers for an organization. If these servers suffer from a common misconfiguration, they may allow any customers to download the entire contents of a given domain, revealing all of the hostname-IP mapping for that domain. This functionality is typically restricted to backup DNS servers who store copies of the DNS zone files, but if this restriction is not set, then anyone can dump the zone remotely via a DNS zone transfer.

Performing a DNS zone transfer is simple using the nslookup utility built into most platforms. We'll demonstrate it using the Windows nslookup client below. First, we start the nslookup client, then specify the DNS server we wish to query (should be authoritative for the target zone), and dump the contents of the zone with the ls-domain argument.

```
C:\nslookup
Default Server: internal
Address: 10.1.1.65
```

```
> server nsl.victim.com
Default Server: nsl.victim.com
Address: 192.168.15.77
```

```
> ls -d victim.com
```

# Hacking Exposed Web Applications

```
@ IN SOA victim.com. root.freebsd.victim.com. (
961230 ; Serial
3600 ; Refresh
300 ; Retry
3600000 ; Expire
3600 ) Minimum victim.com.

IN NS freebsd.victim.com.
```

```
mail.victim.com. MX 10.0.0.10 ; mail
www.victim.com. IN A 10.0.0.2 ; web
app.victim.com. IN A 10.0.0.1 ; web app 1
```

From this query, we discovered Web servers and other application servers that are accessible via DNS.

# Ping

The most basic approach to server discovery is to send ICMP Echo Requests (typically implemented via the ping utility) to potentially valid hostnames or IP addresses. Numbered tools for performing pings exist, and many are bundled into port scanning tools, which we discuss.

# Discovery Using Port Scanning

One of the most effective mechanisms for discovering servers is port scanning. A port scan attempts to connect to specific TCP or UDP ports to determine if a service exists.

The most basic approach to server discovery is to send ICMP Echo Requests (typically implemented via the ping utility) to potentially valid hostnames or IP addresses. Numbered tools for performing pings exist, and many are bundled into port scanning tools, which we discuss.

Another way to reduce scan time is to use SYN scans. Instead of completing a three-way TCP handshake, this scanning technique only waits for the SYN/ACK response from the server and moves on without bothering to send the final ACK. This cuts scanning overhead by one-third. Many freely available port scanners have the ability to perform SYN scanning.

Of course, you don't want to sacrifice accuracy for speed. We recommend performing multiple scans to ensure that some random error condition doesn't cause a port to get overlooked. Two to three repetitions are probably sufficient. We also highly recommend continuous scanning over time to ensure that new servers coming online are identified.

One aspect of port scanning that is often inherently inaccurate is UDP scanning. UDP scanning technology sends a single packet to the target UDP port, and then awaits

| Protocol | Port | Service |
| --- | --- | --- |
| TCP | 21 | FTP |
| TCP | 22 | SSH |
| TCP | 23 | Telnet |
| TCP | 25 | SMTP |
| TCP | 53 | DNS |
| TCP | 80 | HTTP |
| TCP | 110 | POP |
| TCP | 111 | RPC |
| TCP | 139 | NetBIOS Session |
| TCP | 389 | LDAP |
| TCP | 443 | SSL |
| TCP | 445 | SMB |
| TCP | 1433 | SQL |
| TCP | 2049 | NFS |
| TCP | 3389 | Terminal Server |
| UDP | 53 | DNS |
| UDP | 69 | TFTP |
| UDP | 137 | NetBIOS Name |
| UDP | 138 | UDP Datagram |
| UDP | 161 | SNMP |
| UDP | 500 | IKE |

Table 2-2. Common TCP and UDP Ports Used for Server Discovery

Another way to reduce scan time is to use SYN scans. Instead of completing a three-way TCP handshake, this scanning technique only waits for the SYN/ACK response from the server and moves on without bothering to send the final ACK. This cuts scanning overhead by one-third. Many freely available port scanners have the ability to perform SYN scanning.

One aspect of port scanning that is often inherently inaccurate is UDP scanning. UDP scanning technology sends a single packet to the target UDP port, and then awaits

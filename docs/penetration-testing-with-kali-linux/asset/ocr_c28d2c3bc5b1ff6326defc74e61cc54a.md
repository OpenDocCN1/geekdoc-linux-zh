# OffSec

Penetration Testing with Kali Linux

of megacorp.com configured PTR^249records for the domain, we could scan the approximate results with reverse lookups to identify the hostname for each IP.

Let's use a loop to scan IP addresses 512.221.169.200 through 512.221.169.254. We will filter out invalid results (using grep -v) by showing only entries that do not contain "found".

```
208.222.51.in-addr.arpa domain pointer megacorp.com.
289.222.51.in-addr.arpa domain pointer beta.megacorp.com.
219.222.51.in-addr.arpa domain pointer fs1.megacorp.com.
211.222.51.in-addr.arpa domain pointer intranet.megacorp.com.
212.222.51.in-addr.arpa domain pointer mail.megacorp.com.
213.222.51.in-addr.arpa domain pointer mail2.megacorp.com.
214.222.51.in-addr.arpa domain pointer router.megacorp.com.
215.222.51.in-addr.arpa domain pointer siem.megacorp.com.
216.222.51.in-addr.arpa domain pointer smtp.megacorp.com.
217.222.51.in-addr.arpa domain pointer syslog.megacorp.com.
218.222.51.in-addr.arpa domain pointer support.megacorp.com.
219.222.51.in-addr.arpa domain pointer test.megacorp.com.
220.222.51.in-addr.arpa domain pointer vpn.megacorp.com.
```

List 45 - Using Bash to brute force reverse DNS names

We managed to resolve a number of IP addresses to hold reverse lookups. If we were performing an assessment, we could further extrapolate these results, and scan for "mail2", "router", and reverse-lookup positive results. These types of scans are often cyclical, we expand our search based on any information we receive at every turn.

Now that we have our foundational DNS enumeration skills, let's explore how we can automate the process using a few applications.

There are several tools in Kali Linux that can automate DNS enumeration. Two notable examples are DNSRe256 and DNSenum; let's explore their capabilities.

```
kali@kali:~ dnsrecon -d megacorp.com -t std
[*] std: Performing Enumeration against: megacorp.com...
[*] DNSenum is not configured for megacorp.com...
* SOA ns1.megacorp.com 51.79.37.18
* NS ns5.megacorp.com 66.178.287
* NS ns3.megacorp.com 51.222.39.63
* NS ns2.megacorp.com 512.221.169.212
* MX mail1.megacorp.com 512.221.169.212
* MX spool.mail.gandi.net 217.70.178.1
* MX fb0.mail.gandi.net 217.78.178.217
```

> ^249 (Wikipedia, 2022), from en.wikipedia.org/wiki/Reverse_DNS_Lookup

> ^250 (Copyright, 2023), https://github.com/darkoper/dnsrecon

PWK - Copyright 2023 OffSec Services Limited. All rights reserved.

135
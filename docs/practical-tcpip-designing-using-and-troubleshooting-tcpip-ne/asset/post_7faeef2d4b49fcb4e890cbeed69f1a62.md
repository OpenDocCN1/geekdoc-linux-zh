
## 9.2 Debug output for a failed name resolution

The most common problem with a DNS configuration that has been working correctly is that you try to look up a name but it can't be resolved. Below is the **tcpdump** trace of the DNS traffic for “**ping junk.example.com**” which will query for a name that we know doesn't exist. The names queried are just what we expect, given that our PC has its searchlist setting as **uit.co.uk**.

```
192.0.2.17.3569 > 192.0.2.19.53:  53790+ A? junk.example.com. (34)
192.0.2.19.53 > 192.0.2.17.3569:  53790 NXDomain 0/1/0 (106)
192.0.2.17.3569 > 192.0.2.19.53:  53791+ A? junk.example.com.uit.co.uk. (44)
192.0.2.19.53 > 192.0.2.17.3569:  53791 NXDomain* 0/1/0 (104)
```

Let’s say we want to explore what’s happening in more detail with this failing resolution. We run **tcpdump** and **nslookup -d** at the same time:

```
192.0.2.17.3571 > 192.0.2.19.53:  33590+ PTR? 19.2.0.192.in-addr.arpa. (45)
192.0.2.19.53 > 192.0.2.17.3571:  33590* 1/1/0 PTR res3lx.uit.co.uk. (126)
192.0.2.17.3571 > 192.0.2.19.53:  33591+ A? junk.example.com. (34)
192.0.2.19.53 > 192.0.2.17.3571:  33591 NXDomain* 0/1/0 (95)
192.0.2.17.3571 > 192.0.2.19.53:  33592+ A? junk.example.com.uit.co.uk. (44)
192.0.2.19.53 > 192.0.2.17.3571:  33592 NXDomain* 0/1/0 (104)
```

There are a few points worth noting:

- **nslookup** always queries for the name of the DNS server it’s using, so we expect the reverse lookup shown at the beginning of the above traces. (As we mentioned in Module 7.5, if the reverse lookup fails, **nslookup** terminates, which is why many people prefer to use other **host** or **dig** instead.)
- after the query for **junk.example.com** failed because the name didn't exist, **nslookup** then tried **junk.example.com.uit.co.uk** as expected.

Now let’s see what “**host -v**” does. Below is the **tcpdump** trace (we haven’t shown **host** for lack of space because it isn’t just a simple name’s output):

```
192.0.2.17.3579 > 192.0.2.19.53:  20100+ A? junk.example.com. (34)
192.0.2.19.53 > 192.0.2.17.3579:  20100 NXDomain 0/1/0 (106)
```

Because the name you’re looking up isn’t just a simple name, **host** queries only for the name exactly as you entered it. This is an important point: both **nslookup** and **host** refer to the resolver configuration files but do *not* use the standard resolver code. This makes testing difficult. If you really need to look at a resolution problem on this level, we recommend you:

- 1. run “**tcpdump -n**” as always
- 2. a. use **ping**, not **nslookup** or **host**, to generate the lookup. **ping** uses your machine’s standard resolver so it will generate the same queries that any other standard application would
  b. append a dot to the name you’re querying, e.g. “**host junk.example.com.**” so that it’s interpreted as an FQDN and some or all of the domain or explicit searchlist activity is bypassed. If the name you’re querying is internal, e.g. “**alice**, append your domain name manually yourself, and add the dot, as in “**host alice.example.com.**” Then you’ll know exactly what’s what.

However, for ordinary day-to-day checking of DNS names, etc., **host** is just fine.

```
alice% nslookup -d junk.example.com
;; res_nmkquery(QUERY, 19.2.0.192 in-addr.arpa, IN, PTR)

Got answer:
HEADER:
opcode = QUERY, id = 33590, rcode = NOERROR
header flags: response, auth, answer, want recursion, recursion avail
questions = 1, answers = 1, authority records = 1, additional = 1
QUESTIONS:
19.2.0.192 in-addr.arpa, type = PTR, class = IN
ANSWERS:
-> 19.2.0.192 in-addr.arpa
name = res3lx.uit.co.uk
ttl = 86400 (1D)
AUTHORITY RECORDS:
-> 2.0.192 in-addr.arpa
nameserver = res3lx.uit.co.uk
ttl = 86400 (1D)
ADDITIONAL RECORDS:
-> res3lx.uit.co.uk
internet address = 192.0.2.19
ttl = 86400 (1D)

Server: res3lx.uit.co.uk
Address: 192.0.2.19

;; res_nmkquery(QUERY, junk.example.com, IN, A)

Got answer:
HEADER:
opcode = QUERY, id = 33591, rcode = NXDOMAIN
header flags: response, auth, answer, want recursion, recursion avail
questions = 1, answers = 0, authority records = 1, additional = 0
QUESTIONS:
junk.example.com, type = A, class = IN
AUTHORITY RECORDS:
-> example.com
ttl = 21600 (6H)
origin = dns1.icann.org
mail addr = hostmaster.icann.org
serial = 2002020400
refresh = 7200 (2H)
retry = 3600 (1H)
expire = 1209600 (2W)
minimum ttl = 21600 (6H)

;; res_nmkquery(QUERY, junk.example.com.uit.co.uk, IN, A)

Got answer:
HEADER:
opcode = QUERY, id = 33592, rcode = NXDOMAIN
header flags: response, auth, answer, want recursion, recursion avail
questions = 1, answers = 0, authority records = 1, additional = 0
QUESTIONS:
junk.example.com.uit.co.uk, type = A, class = IN
AUTHORITY RECORDS:
-> uit.co.uk
ttl = 86400 (1D)
origin = res3lx.uit.co.uk
mail addr = hostmaster.uit.co.uk
serial = 167
refresh = 10800 (3H)
retry = 3600 (1H)
expire = 604800 (1W)
minimum ttl = 86400 (1D)
*** res3lx.uit.co.uk can't find junk.example.com: Non-existent host/domain
```

find the *name* of the DNS server we're using

*query* for the name exactly as we entered it

no A record found for this name so answer = 0 and mode (response) is NXDOMAIN

the first query failed, so see if we can find the name with our domain name appended to it

no A record found for this name either

### 9.3 DNS problems and causes

This module concentrates on the types of DNS problems that can occur and how you can identify them.

- 1. DNS relies on all your underlying networking infrastructure. If your basic connectivity and routing don't work, neither will DNS. You can prove that 99% of your networking is OK by:
  - a. **pinging** any host on your LAN, by IP number
  - b. **pinging** any host on the Internet, by IP number

- 2. your client is wrongly configured:
  - see if the same problem occurs on another machine that is configured similarly (using the same DNS servers). If it doesn't, the problem lies somewhere on the first machine.
  - run **tcpdump** and watch the packets. If there are no DNS packets reaching the wire, your PC is almost certainly not using DNS at all. Check that you configured the resolver with at least one DNS server and that you didn't enter its address as a name instead of an IP number. See also the next module for other name resolution systems that may be interfering.

- 3. your client is configured to use a DNS server on your own directly connected LAN and that server is down. If the whole server machine is down **tcpdump** won't show any DNS packets unless the server has failed in the last few seconds. Instead you'll see ARP requests from the client to the server, and no ARP replies. If only the DNS server has died, **tcpdump** will show DNS queries sent to the server but no DNS replies, only ICMP error messages saying something like "ICMP udp port domain unreachable".

- 4. your ISP's servers are down (assuming that you are not running an internal DNS server of your own, but relying on your ISP's servers), or you're using your own DNS server that's not on the client's directly connected wire. **tcpdump** will show packets going out to the server but none coming back:

```
12:06:50. 939044 192.0.2.38.1025 > 1.2.3.4.53: 6018+ A? www.ibm.com. (29)
12:07:00. 939863 192.0.2.38.1025 > 1.2.3.4.53: 6018+ A? www.ibm.com. (29)
12:07:20. 941742 192.0.2.38.1025 > 1.2.3.4.53: 6018+ A? www.ibm.com. (29)
```

Notice the pattern in the times of the packets. (If you configured more than one DNS server address in the resolver, you'll see several of these patterns intermingled. The precise pattern depends on your implementation, by the way.) The resolver sent queries at times 0 (not shown), 5, 10, and 20 seconds, unless it has received a reply. After sending the last query it waited a further 40 seconds; if no reply is received then it times out and gives an error to the application that asked for the resolution. Potential causes of this problem are:

- you entered the wrong IP address for the server in the resolver configuration (as we did in this example). Check the documentation from your ISP. (The problem *can't* be caused by entering the server address as a name instead of a number. If you did that, the DNS wouldn't even try to contact the server.)
- the server machine is dead. Try **pinging** it.


To make `named.conf` easier to understand and maintain, zones in different View sections can have the same name while having different zone files. Both the local and public View sections in the example have zones named **zach.net**: The public **zach.net** zone file is named **public.net**, while the local one is named **local.net**.

The Logging section is described on page 808.

The zone files defining **zach.net** are similar to the ones in the previous examples; the public file is a subset of the local one. Following the SOA resource record in both files is a TXT, two NS, and two MX resource records. Next are three CNAME resource records that direct queries addressed to www.zach.net, ftp.zach.net, and mail.zach.net to the system named **ns.zach.net**. The next four resource records specify two nameserver addresses and two mail servers for the ns.zach.net domain.

The final four resource records appear in the local **zach.net** zone file and not in the public zone file; they are address (A) resource records for local systems. Instead of keeping this information in `/etc/hosts` files on each system, you can keep it on the DNS server, where it can be updated easily. When you use DNS instead of `/etc/hosts`, you must change the `hosts` line in `/etc/nsswitch.conf` (page 455).

```
$ cat local.net
; zach.net local zone file

    TTL     3D
    @       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        20051118  ; serial
                        8H        ; refresh
                        2h        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      TXT     "Sobell Associates Inc."
        IN      NS      ns ; Nameserver address (unqualified)
        IN      NS      ns.speedy.net. ; Nameserver address (qualified)
        IN      MX      10 mail      ; Mail exchange (primary/unqualified)
        IN      MX      20 mail.max.net. ; Mail exchange (2nd/qualified)

www     IN      CNAME   ns
ftp     IN      CNAME   ns
mail    IN      CNAME   ns

ns      IN      A       192.168.0.1
        IN      A       192.168.0.6
        IN      MX      10 mail
        IN      MX      20 mail.max.net.

speedy  IN      A       192.168.0.1
grape   IN      A       192.168.0.3
potato  IN      A       192.168.0.4
peach   IN      A       192.168.0.6
```

The public version of the **zach.net** zone file follows:

```
$ cat public.net
; zach.net public zone file
;
$TTL    3D
@       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        20051118  ; serial
                        8H        ; refresh
                        2H        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      TXT     "Sobell Associates Inc."
        IN      NS      ns ; Nameserver address (unqualified)
        IN      NS      ns.speedy.net. ; Nameserver address (qualified)
        IN      MX      10 mail      ; Mail exchange (primary/unqualified)
        IN      MX      20 mail.max.net. ; Mail exchange (2nd/qualified)

www     IN      CNAME   ns
ftp     IN      CNAME   ns
mail    IN      CNAME   ns
ns      IN      A       192.168.0.1
        IN      A       192.168.0.6
        IN      MX      10 mail
        IN      MX      20 mail.max.net.
```

There are two reverse zone files, each of which starts with SOA and NS resource records followed by PTR resource records for each of the names of the servers. The local version of this file also lists the names of the local systems:

```
$ cat named.local
; "0.168.192.in-addr.arpa" reverse zone file
;
$TTL    3D
@       IN      SOA     ns.zach.net. mgs@sobell.com. (
                        2005110501  ; serial
                        8H        ; refresh
                        2H        ; retry
                        4W        ; expire
                        1D )      ; minimum

        IN      NS      ns.zach.net.
        IN      NS      ns.speedy.net.
1       IN      PTR     gw.zach.net.
1       IN      PTR     www.zach.net.
1       IN      PTR     ftp.zach.net.
1       IN      PTR     mail.zach.net.
1       IN      PTR     speedy.zach.net.
3       IN      PTR     grape.zach.net.
4       IN      PTR     potato.zach.net.
6       IN      PTR     peach.zach.net.
```

## CHAPTER SUMMARY

DNS, which maps domain names to IP addresses, and vice versa, is implemented as a hierarchical, distributed, and replicated database on the Internet. Although BIND, which implements DNS, has security issues, you can improve its security by running it inside a chroot jail and using transaction signatures (TSIGs) and SELinux.

When a program on the local system needs to look up an IP address that corresponds to a domain name, it calls the resolver. The resolver queries the local DNS cache, if available, and then queries DNS servers on the LAN or Internet. There are two types of queries: iterative and recursive. When a server responds to an iterative query, it returns whatever information it has at hand; it does not query other servers. Recursive queries cause a server to query other servers if necessary to respond with an answer.

There are three types of servers. Master servers, which hold the master copy of zone data, are authoritative for a zone. Slave servers are also authoritative and copy their data from a master server or other slave servers. DNS caches are not authoritative and either answer queries from cache or forward queries to another server.

The DNS database holds resource records for domains. Many types of resource records exist, including A (address), MX (mail exchange), NS (nameserver), PTR (pointer for performing reverse name resolution), and SOA (start of authority, which describes the zone).

## EXERCISES

- 1. What kind of server responds to recursive queries?
- 2. What kind of DNS record is likely to be returned when a Web browser tries to resolve the domain part of a URL?
- 3. What are MX resource records for?
- 4. How would you find the IP address of example.com from the command line?
- 5. How would you instruct a Linux system to use the local network's DNS cache, located at 192.168.1.254, or the ISP's DNS cache, located on 1.2.3.4, if the LAN nameserver is unavailable?
- 6. How would you instruct a DNS server to respond only to queries from the **137.44.*.*** IP range?
- 7. How might a resolver attempt to find the IP address of the **example** domain?

### Advanced Exercises

- 8. How would you set up a private domain name hierarchy that does not include any of the official InterNIC-assigned domain names?
- 9. Which part of DNS is most vulnerable to an attack from a malicious user and why?
- 10. It is often irritating to have to wait for DNS records to update around the world when you change DNS entries. You could prevent this delay by setting the TTL to a small number. Why is setting the TTL to a small number a bad idea?
- 11. Outline a method by which DNS could be used to support encryption.

## 25 iptables: Setting Up a Firewall

### IN THIS CHAPTER

- How iptables Works
- Rules, matches, targets, and chains
- Network packet
- Jumps and targets
- JumpStart: Building a Firewall Using system-config-firewall
- Anatomy of an iptables Command
- Building a Set of Rules
- system-config-firewall: Generates a Set of Rules
- Sharing an Internet Connection Using NAT

The **iptables** utility builds and manipulates network packet filtering rules in the Linux kernel. You can use **iptables** to create a firewall that protects a system from malicious users and to set up NAT (Network Address Translation, page 1095), which can allow multiple systems to share a single Internet connection. The **iptables** utility is flexible and extensible, allowing you to set up both simple and complex network packet filtering solutions. It provides connection tracking (stateful packet filtering), allowing you to handle packets based on the state of their connection. For example, you can set up rules that reject inbound packets trying to open a new connection and accept inbound packets that are responses to locally initiated connections. Features not included in the base **iptables** package are available as patches via the patch-o-matic program.

Some of the concepts required to fully understand **iptables** are beyond the scope of this book. Although you can use **iptables** at several different levels, this chapter presents only the fundamentals. There are, however, some sections of this chapter that delve into areas that may require additional understanding or explanation. If a concept is not clear, refer to one of the resources in “More Information” on page 822.

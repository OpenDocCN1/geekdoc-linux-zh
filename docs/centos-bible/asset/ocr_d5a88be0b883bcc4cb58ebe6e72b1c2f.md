NS (which stands for "Name Server") records in the parent zone for a domain list the primary and one or more secondary name servers. This *delegation* of servers defines the servers that have authority for the zone.

Because zone records change as you add, remove, or reconfigure the computers in the zone, you assign *expiration* times for information about your zone. You set the expiration time in the time-to-live (TTL) field, in the *named.conf* file (which I describe later).

Other specialized types of DNS servers are possible as well. Although these types of servers don't have authority for any zones, they can prove useful for special purposes.

+   ■  **Caching Name Server** —This type of server simply caches the information it receives about the locations of hosts and domains. It holds information that it obtains from other authoritative servers and reuses that information until the information expires (as set by the TTL fields).

> NOTE  The *caching-nameserver* package in CentOS automatically sets up a caching instance of *bind* for instant use in an office or home environment where you don't want to rely on your ISP's name servers.

+   ■  **Forwarding Name Server** —Creating a server that's not authoritative for a zone but that can forward name server requests to other name servers may prove beneficial. This server is essentially a caching name server but is useful in cases in which computers lie behind a firewall and in which only one computer can make DNS queries outside that firewall on behalf of all the internal computers.

# Understanding Alternative Zones

As an administrator of a DNS server, you need to configure several zones. Each zone represents part of the DNS namespace as you view it from your DNS server. Besides the one or more zones representing your domain, you have a zone that identifies your local host and possibly your local, private LAN.

If you configure a server as authoritative for a zone, that server has the last word on resolving addresses for that zone. In the upcoming "DNS Name Server Example" section, your primary master name server is authoritative for the domain you control (as are the secondary name servers it passes its records to), but not for domains outside your domain.

Remember that the DNS server that you configure is the ultimate authority for your zone. Other zones don't know how you configure your hostnames and IP addresses unless you properly set up your DNS server to distribute that information across the Internet.

The definitive data that you set up for your domain exists in the form of resource records. *Resource records* consist of the data associated with all names below the authoritative point in the tree structure. When the DNS server uses these records to reply to queries, it sets the *authoritative answer* (AA) bit in the packet that includes the reply. The AA bit indicates that your name server has the best and most current information available about your domain.
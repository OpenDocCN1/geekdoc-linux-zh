DNS was based on the fact that management control belonged to zone masters, which in turn introduced the authority concept. With the introduction of the DNS database, NIC was no longer responsible for all the addresses on the Internet. NIC's role now was to control the top-level names and maintain a stable and complete DNS database. In addition, all authoritative domain name servers had a full copy of the DNS database, which reduced the load on the NIC servers and assured faster name lookup for all hosts.

# Zones Versus Domains

Many people confuse zones with domains. A zone is a subset of a certain domain in which the name server of this zone has authority over a subset of this domain. For example, say there are six name servers: A, B, C, D, E, and F. A is the top-level name server; B and C are at the next level; D and E are sub-domains of C; and F is a sub-domain of E (see Figure 14.1).

# FIGURE 14.1

In zone C, the C administrator manages the whole C branches and the C domain encompasses all the hosts in the C branches.

![](bbox=[0.35, 0.38, 0.78, 0.78])

If the C domain administrator manages the branches of the C domain, C can be considered a zone. In other words, zones are hosts rooted to a higher-level domain in which they share administration privileges.

# DNS Clients

DNS plays an important role in your daily Internet life. If you want to access Yahoo, for example, you write http://www.yahoo.com in the address bar of your browser and the browser opens the site. This might seem simple, but a lot had to happen for this to occur. When you typed the address and pressed Enter, the browser first tried to resolve the address you typed in. This process is called hostname resolution and is executed through the standard C library with which your SuSE Linux comes equipped. A special routine in the C library contacted your name server and the following scenario happened:

The browser used a gethostname() C function and queried the IP address of http://www.yahoo.com. The resolver scanned the configuration file /etc/resolve.conf to find out where it would locate the IP. If the resolve.conf file specified a name server to be looked up, the resolver would query the name server. The name server would then pass the
# Additional Network Services Considerations

For Linux routers acting as gateways, the network designer must determine what additional services should be run on the gateway. The additional services are based on need, expense, and management.

# Email

Mail services are often run on the Linux gateway to provide mail delivery, especially to the Internet.

Linux does a very nice job of handling mail services, which might prove to be an ideal solution for a corporate mail system.

Gateways to the Internet should be considered carefully. Placing the mail server on the pppd server leaves the mail server open should the gateway be compromised.

# Domain Name Services (DNS)

DNS is often a good candidate for running on the same gateway as pppd. Like a mail server, the DNS server (usually BIND), also is open to attack; however, DNS is not considered as risky as email for several reasons: It is less interesting to hackers, traditionally has fewer holes than mail servers (although this trend is subsiding as mail servers are continually being hardened), and typically only brings about a denial of service as opposed to a threat to resources.

A DNS server run in cache-only mode can be useful for both corporate and Internet gateways. A cache-only server simply caches all entries requested for later use. This saves query time for the next user that requests the particular host name and keeps the additional traffic off the gateway's WAN link.

For corporate gateways, it is worth considering loading the internal domains on the name server as well. This allows name server resolution to occur locally, as opposed to sending the request over the WAN link. There is a small additional load created by the name server pulling the zones on a timed basis, but the load is typically small and is often worth the trade-off if more than a few internal name resolution requests are required.

Placing a DNS server does have risks, though; and, like email, should be considered carefully to ensure that the advantages gained are worth the risk.

# Web Caching

Web caching, like DNS, might be considered for both Internet and corporate connections. Under best circumstances, a 5%-10% hit rate can be expected on visited pages in larger sites. Many current web caching solutions allow predefined sites to be cached and common pages to be "mirrored," which can be very effective for storing local copies of corporate intranet sites.
| | |
| --- | --- |
| 2 | Link | Messages stay within the router's group. The routers never let these messages pass through. |
| 5 | Site | As defined by the network administrators, the messages stay within the site's locality. |
| 8 | Organization | As defined by the network administrators, the messages stay within the organization's locality. |
| 14 | Global | All routers permit messages to pass through the global network (until they expire). |

Lastly, the rules for routing (as described in Chapter 17) remain the same. IPv6 uses IPv4's optional IGMP to pass on the request to join or drop a multicast group. Because both use the MAC address to get multicast messages, IPv6 did not have to define anything beyond IPv4's implementation.

The procedure for joining an IPv6 multicast group is almost the same as the IPv4, but you need to use a different structure for selecting the address:

```
/* ********************************** */
/** IPv6 multicast structure definition **** */
/* ********************************** */
struct ipv6_mreq
{
    struct in6_addr ipv6mr_multiaddr; /* IPv6 multicast addr */
    unsigned int ipv6mr_interface; /* interface number */
};
```

The first field, ipv6mr_multiaddr, is the broadcast message address. You place the IPv6 address in this field (for example, FF02::10). The next field is the interface number: 0 means all interfaces, 1 for the first interface (eth0), and so on.

To enable IPv6 multicasting, use the following code snippet:

```
/***** */
/** Join a IPv6 multicast group **** */
/***** */
const char *GroupID = "FF02::4590:3A0";
struct ipv6_mreq mreq;
if ( inet_pton(GroupID, &mreq.ipv6mr_multiaddr) == 0 )
panic("address ($s) bad", GroupID);
mreq.ipv6mr_interface = 0; /* any interface */
if ( setsockopt(sd, SOL_IPV6, IPV6_ADD_MEMBERSHIP, &mreq, sizeof(mreq)) != 0 )
panic("Join multicast failed");
if ( setsockopt(sd, SOL_SOCKET, SO_REUSEADDR, &on, sizeof(on)) != 0 )
panic("Can't reuse address/ports");
```

As you can see, the code is very similar to the IPv4 multicasting code.

# Summary: Moving Your Code into the Future

IPv6 answers the limitations currently found in the IPv4's addressing structure. By extending the addressing range several orders of magnitude, IPv6 appears to be the clear future for the Internet. Still in its infancy, the addressing allocation has adopted standard networks, such as IPX. It already has support in European and Far Eastern networks.
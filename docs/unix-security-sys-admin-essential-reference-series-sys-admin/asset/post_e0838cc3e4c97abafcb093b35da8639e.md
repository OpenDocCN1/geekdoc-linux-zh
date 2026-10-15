
In the remote computing situation, the security perimeter can consist of several extensions. For example, the modems used to establish the link may be encrypting modems, which encrypt packet information prior to transmitting it on the line (though, this technology is expensive). The actual data on the hard disk of the remote computer could also be encrypted. Then if the computer were stolen, the data would be meaningless unless the user had left the decryption key with the computer.

## The Building Materials: Firewall Architecture

Once you’ve defined your security perimeter, the next issue is whether and how a firewall can be built to protect it. Different types of firewalls are appropriate to different circumstances: the type of firewall to be used should be matched to the problem or to the security policies that the organization wishes to enforce. In this section, I examine the major types of firewalls, explaining what they are, how they perform, and any known pitfalls. I won’t make recommendations, since what works in one situation may not work in another.

## The Gate and Choke

The gate in a network functions like a gate in a fence: it allows data to pass between the Internet and the private network. The choke is the opposite: it typically blocks all packets from the Internet to the private network, unless they are destined for the gate, and blocks all packets going from the private network to the Internet, unless they are destined for the gate. The choke is like a fence around a queue at an amusement park: there is only one entrance to the ride and all attempts to go around the queue are blocked by the fence.

The gate and the choke can exist on separate computers or on the same computer. There can be multiple gates (e.g., one for each supported protocol) or there can be one gate. Multiple gates provide a small measure of increased security, but this is countered by the extra complexity and administration involved.

The gate and the choke are built into many different firewalls. For a truly effective firewall, both must be present.

## The Air Gap

The air gap is probably the best firewall that can be devised, and it is used by many security and law enforcement agencies. In air gap implementation, any computer connected to the Internet cannot be connected to any other computer or network in the organization. While this may sound paranoid, it means that break-ins and viruses can affect only the systems connected to the Internet. Since these machines are not connected to any other host in the organization, the attacker cannot proceed any further.

An air gap creates a problem with respect to getting useful information to the users in the organization. The problem can be solved in one of two methods: by hand or by disk. The first method, by hand, involves printing the relevant information and then typing it back in on a machine that is connected to the network. The advantage here is that the “seal” is very tight: no air or viruses being carried in the air can escape into the internal network. The second method involves saving the information to a disk, copying it back onto a networked system, and then distributing the information from that system.

While these methods provide very tight security, they will also frustrate and alienate the users in the organization unless there is a very specific need for such heavy security. Users want to be able to correspond with colleagues on the Internet, and the prospect of having to re-input all of their information in order to send it out is not one they will welcome.

## The Screening Router

The screening router is a basic component of most firewalls. It can be either a commercial router or a host-based router with some form of packet-filtering capability. Many screening routers are able to block traffic between networks, between specific hosts, or on an IP port level. The screening router is situated between the Internet and the private network (Figure 11.1).

A filter is used to monitor packets and decide which ones will be allowed past the router. The filter can allow or deny both inbound and outbound packets. Thus, the system administrator can not only deny packets coming from a particular external host, but also prevent connections to specific external systems from an internal machine.

The filter can also allow or deny connections to a particular IP service port. Thus, you could block telnet or rlogin services while allowing FTP connections to an anonymous ftp server. Setting up packet filtering can be a frustrating and even dangerous experience. Developing an effective packet filtering configuration requires intimate knowledge of the TCP and UDP service ports. If the tables are inadvertently misconfigured, the packet filtering implementation may actually make it easier for vandals to gain access.

Morningstar Technologies has built packet filtering capabilities into its PPP implementation (Figure 11.2). These capabilities allow the system administrator to permit or deny certain types of traffic. To prevent or restrict traffic flow, you must be able to anticipate what will be coming in over your router. Whatever the mechanism, many firewalls consist of nothing more than a screening router between the private network and the Internet. The pitfall is that this makes the network highly vulnerable to attack. Since there is direct communication from the Internet to the private network, the exposure in the event of an attack is equal to the number of hosts in the network. Furthermore, unless each host is being regularly examined for attack, the likelihood of an attack being discovered is low.

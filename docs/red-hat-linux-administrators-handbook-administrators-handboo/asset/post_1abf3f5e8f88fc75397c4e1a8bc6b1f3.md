
## Get the Latest Security News

Being informed about what security problems are out there in the world helps you to keep a step ahead of the bad guys who might want to attack your systems. As soon as you know about a security issue that might affect your system, take immediate action before it is too late. You should subscribe to reputable security alert resources, available on the Internet. Here are two.

### CERT

Computer Emergency Response Team (CERT) regularly issues advisories on computer security matters. Subscribe to its mailing list as soon as possible. Visit its Web site at http://www.cert.org/ for details.

### BUGTRAQ@NETSPACE.ORG

BUGTRAQ is another mailing list to which you can subscribe to access daily reports on security issues. Visit its Web site at http://www.netspace.org/lsv-archive/bugtraq.html for details.

## Network Security

### Designing a Secure Network

As a network grows, implementing security as an afterthought becomes more difficult. Users grow accustomed to patterns of usage, poor choices become accepted handicaps, and the administrator must play political games to make changes. These are some of the reasons security of your network as a whole must be examined as you plan the topology.

### Using private IP addresses

The simplest way to maintain security on a network is to ensure that hosts on your network cannot contact, nor be contacted by, the outside world. The easiest way to achieve this would be to never connect them to a public network such as the Internet. This security-through-isolation strategy is not an acceptable restraint in many situations. Using private IP addresses is an easy way of allowing your users to reach the Internet while holding off the bad guys from getting to the user machines privately. RFC 1918 specifies blocks of IP addresses that may be used within a local TCP/IP network but may not traverse Internet routers. These groups of IP addresses are commonly called LAN IP addresses or private IP addresses. Because these IP addresses do not route across the Internet, you do not need to register to use them. By assigning an IP address from within this range, you effectively limit traffic to and from the computer to the local network. This is a quick and effective way of denying outside access to computers while allowing traffic to flow between your internal computers.

The blocks of private IP addresses are the following:

- 10.0.0.0 - 10.255.255.255
- 172.16.0.0 - 172.31.255.255
- 192.168.0.0 - 192.168.255.255

Remember that traffic coming from a private IP address is not able to traverse Internet routers, which means that any computer assigned a private IP address is unreachable by computers outside your network. However, this approach also has the effect of not allowing your users to talk to the outside world. IP masquerading is the solution for this.

### Masquerading IP addresses

Private IP addresses are not routable in the Internet and therefore systems using private IP addresses cannot reach the Internet. You can solve this problem by placing an IP masquerading Red Hat Linux server. With IP masquerading in place, as a packet leaves a user computer, it has the “source address” of its own IP address. As the packet travels through the Red Hat server toward the outside world, it is transformed. The source address of the packet is changed to the address of the Red Hat server, which is a fully routable IP address. The Red Hat server also makes a note of which source address contacted which destination on the Internet. When the packet is sent to the Internet, it is fully capable of reaching its destination and getting a response.

This setup has one catch. Because the source address of the packet is set to the IP of the Red Hat server and not to the user machine behind the server, the response from the foreign computer is sent to the Red Hat server. Therefore, to complete the packet transmission, the Red Hat server has to search a table to see which machine this packet belongs to. It then sets the source address of the packet to the address of the private user computer and sends the packet to that computer. Voilà, a round trip across the Internet has been made from a machine with a private IP address. IP masquerading is also known as network address translation (NAT).

From the user's standpoint, the user has an Internet connection that appears to be fully routable. The security comes from the table that the Red Hat server keeps of which user computers are talking to which foreign Internet sites. If some bad guy wants to gain access to one of your user computers, he will be unable to. The only IP address ever seen by the outside world is the address of the Red Hat server, and not all the addresses behind it. Even if the bad guy sends a packet to the Red Hat server, the server would have no way of knowing which user machine to forward it to.

By default, the Red Hat Linux kernel has IP masquerading support built in. However, if you have removed such support earlier or are using a kernel that does not have IP masquerading built in, you need to recompile the kernel, load a few modules, and set a packet-filtering rule to allow the address translation to occur. For IP masquerading to work, you need to enable IP forwarding service on the server. You can enable IP forwarding (for the default kernel shipped by Red Hat) by setting FORWARD_IPV4 to yes in the /etc/sysconfig/network file. This discussion assumes that you are using a kernel with IP masquerading and forwarding support built in, and that you have also installed the ipchains package on the Red Hat server.

To connect your internal network to the outside world, you need two network interfaces on the IP masquerading server. One interface will be used to connect to the internal network, and the other interface will be used to connect the server (and the internal network via IP masquerading) to the outside world. Because such a server has multiple interfaces, it is often called a *multihomed* server. You can assign a private IP address to the network card connected to the internal network. For example,

```
/sbin/ifconfig eth1 inet 192.168.1.1 netmask
255.255.255.0
```

This assumes that your network interface for the internal network is eth1 and that you will be running fewer than 253 user computers within your network. If you are in a situation where you will have more than 253 user computers, you may use a netmask of 255.255.0.0, which allows more than 65,000 user computers behind one Red Hat IP masquerade computer. If you exceed 253 user computers, set up a second IP masquerade computer and divide your network into two subnets.

By configuring your user computers with IP addresses starting at 192.168.1.2 and ending at 192.168.1.254, and by assigning them all a gateway of 192.168.1.1 and a subnet mask of 255.255.255.0, you should be able to ping the gateway (192.168.1.1) from each user computer.

At this point, all the user machines can talk to each other and to the Red Hat server, but you still can't reach the outside world from a client machine until you define a filter rule on the Red Hat server. After you enter the following commands, you should be able to browse and communicate from a user machine as if you were directly connected to the Internet:

```
/sbin/ipchains -A forward -j MASQ -s 192.168.0.0/24 -d 0.0.0.0/0
/sbin/ipchains -P forward DENY
```

The first command enables IP masquerading service for all IP packets that have a destination other than the 192.168.0.0 network. It forwards masqueraded IP packets originating from the 192.168.0.0 network to the default route to the network attached to the other interface. The second command sets the default forwarding policy to be deny for all packets not originating from the internal network. Put these commands into /etc/rc.d/rc.local so that IP masquerading will begin when you boot the Red Hat server.

## What Is a Firewall?

Sometimes, you may not want the all-or-nothing approach achieved by using private IP addresses. You may want to give the general public access to browse Web sites on your Web server, but no other type of access. Or, you may have a policy restriction that limits employee use of the Internet to e-mail only. Both of these examples are situations in which a firewall would fit perfectly.

A firewall is a computer intended to enforce your policies about what type of traffic is allowed to pass from the public network to the private network. Most often, a firewall is placed between a private intranet and the Internet to allow traffic to pass that meets certain criteria while denying the rest. Firewalls can be very open, allowing nearly all traffic through, or they can be very restrictive, permitting very limited use. The firewall administrator controls all of this through configuration of rule sets.

It is wise to dedicate a computer solely to the task of being the firewall. If you are relying on your firewall to control access to your internal network, then make sure your firewall is as secure as possible. This machine


## 5.11 ICMP redirects implementations; automatic routing protocols

### Linux route command and routing table flags

The Linux manpage documents two flag types (in addition to the U, G, and H entries we saw in Module 5.2) that indicate whether the entry was created:

- a. normally (manually, or via **ifconfig** or the default gateway setting), or
- b. automatically by some component of the system itself.

The flags are shown in Table 5.1. However, most current versions of Linux *don't* include the routes created by ICMP redirects in the default listing. The manpage is describing what happens on other versions of UNIX. To see these extra entries on Linux you have to use the command
```c
route -n -C
```
which displays the *routing table cache*. (But this doesn't display the D flag either.)

| Flag | If present | If absent |
| :--- | :--- | :--- |
| **D** | D**ynamic**: this entry was created automatically from an ICMP redirect or by a routing daemon (see below) | normal (manually configured) entry |
| **M** | **M**odified by an ICMP redirect or a routing daemon | normal (manually configured) entry |

Table 5.1 Two Linux manpage flags

### ICMP redirect notes

There are a few more features relating to ICMP redirects that you may need to know:

- 1. the RFCs say that routers may legitimately choose to ignore redirects. If Alice is configured as a router, what we described in the previous module may not work
- 2. Windows-NT doesn't show ICMP-created routes in its routing tables. There's no convenient way to display them
- 3. after ten minutes Windows-NT removes ICMP-created routes, so if this machine is still sending to that destination, the ICMP redirect procedure will be repeated every ten minutes
- 4. when a Linux host (Alice) receives an ICMP redirect to use a router (Rupert), if Alice doesn't have Rupert already in her ARP cache she won't successfully create the route until she receives the same ICMP redirect a second time. (This doesn't make much difference to the efficiency of the network, but it does clutter the **tcpdump** traces when you're trying to see what's happening.)

### Automatic routing protocols – RIP, OSPF, BGP

(Strictly this doesn't belong here, but it explains what a routing daemon is and how you could get **M**– or **D**–flagged entries in your routing tables.)

All the routing decisions we've considered so far have been like this:

```
if (dest is in range-A)
    send packet via router-1
else if (dest is in range-B)
    send packet via router-2
...
```

A system that uses rules like this and nothing else can't have any resilience. The same action is decided on every time because the rules are completely deterministic. How then do we get resilience on the Internet?

The answer is that resilience is not provided at the IP routing level, but through higher, application-level mechanisms instead. The basic routing operates exactly as we've described, using the routing tables we've seen. However, application programs called *routing daemons* run on the routers and detect when network links go down or come up again, and communicate this information to the corresponding programs on other routers. These programs then modify the routing tables. By separating this adaptive, resilient functionality from the second-to-second packet forwarding, the basic routing can be performed very quickly, which is crucial for high-speed networks.

Using our postal analogy again, the Internet is like messenger boys running to and fro between offices with postcards to be delivered (Figure 5.13). There's a Big Boss (routing daemon) sitting in each office. When he hears from returning messenger boys that they're getting delayed because High Street is closed, he does two things:

- 1. he tells all his boys not to go via High Street, but to use Main Street instead (changes the routing tables on his own router)
- 2. he sends messages to neighboring offices that they should avoid High Street too

Of course, he sends the messages using the boys, but he can give them special instructions. (In this analogy we have to assume that the boys are moronic and never themselves learn not to go down a closed street, which is of course completely unlike any real postal service.)

![](img/a2132b646d336d5f9a21102d6320e537_164_0.png)

Common routing protocols in use are *BGP (Border Gateway Protocol)* used on the Internet backbone, *OSPF (Open Shortest Path First)*, and *RIP (Routing Information Protocol)*, which is old and less flexible than BGP, and has fallen out of favor.

This type of routing is very different from what is needed on a typical internal network, so we discuss it no further (except in the Notes).

## 5.12 Lab – test network to demonstrate ICMP redirects

The best way to see ICMP redirects working would be to construct on your real LAN the network we had in Module 5.10. However, that requires several test machines and we haven't really told you how to configure a network like this yet. The next best way is to use the network in Figure 5.14 but with the IP addresses changed to match your real LAN; the only extra machine you need is a test machine to use as Richard. (You can build a test network with just two machines – Alice and Richard – to see ICMP redirects generated, but you need the bigger networks to see the routing change as a result of the redirects.)

![](img/a2132b646d336d5f9a21102d6320e537_165_0.png)

We're going to configure Alice to use Richard as her default gateway. Then, when Alice sends to an address on the Internet, say 128.9.0.107, the packet goes to Richard, who forwards it to Rupert … Richard will send an ICMP redirect to Alice, saying “use Rupert in future for this address.” (The example is artificial. It’s causing at least one ICMP redirect and a double hop on the first packet to every external address. We did it this way only because it doesn’t need many machines or a lot of configuration to set up.)

- 1. ensure Richard is configured to act as a router (Module 3.6)
- 2. run `tcpdump -n -t -e` on any machine connected to this LAN wire
  - “e” shows the Ethernet addresses, which we need in order to see which router is being used when a packet is forwarded
- 3. Alice:
  - IP address: 10.1.1.11
  - Netmask: 255.255.255.0
  - Default gateway: 10.1.1.22 (i.e. Richard)
- 4. Richard
  - IP address: 10.1.1.22
  - Netmask: 255.255.255.0
  - Default gateway: 10.1.1.254 (i.e. Rupert)
- 5. From Alice, "ping -c1 128.9.0.107" (Linux), "ping -n 1 128.9.0.107" (Windows). Alice sends this using Richard as router
- 6. Richard forwards the packet to Rupert (and tcpdump can't see beyond Rupert, so that's the end of this packet as far as tcpdump is concerned)
- 7. Richard sends an ICMP redirect to Alice, saying "use Rupert (10.1.1.254) in future when trying to reach 128.9.0.107"
- 8. from Alice, again "ping -c1 128.9.0.107" (Linux), "ping -n 1 128.9.0.107" (Windows). This time Alice sends the packet via Rupert, without troubling Richard at all
- 9. on Alice, "route -n" (Linux), "route print" (Windows) shows the current routing tables. The ICMP-created entry isn't shown
- 10. if Alice is running Linux, "route -nC" shows the current routing table cache, which does show ICMP-created entries.

The relevant lines extracted from the tcpdump trace are:

```
00:00:b7:b6:3d:f6 00:50:da:e4:61:34 ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
00:50:da:e4:61:34 00:40:b7:b6:3d:f6 ip 70: 10.1.1.22 > 10.1.1.11: icmp: redirect 128.9.0.107 to host 10.1.1.254
00:50:da:e4:61:34 00:00:c0:1a:aa:6e ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
00:40:b7:b6:3d:f6 00:00:c0:1a:aa:6e ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
```

The output of route -nC in which you can see the temporary route for destination 128.9.0.107 reachable via gateway 10.1.1.254 is:

```
10.1.1.22     10.1.1.255      10.1.1.255      ibl     0       0       0 lo
10.1.1.11     128.9.0.107     10.1.1.254                 0       0       2 eth0
```

### Using names instead of numeric MAC addresses

Working with MAC addresses is awkward because they're so long. On Linux we can store MAC-address-to-name mappings in the file /etc/ethers and then have tcpdump print the addresses as names instead of numbers. Our /etc/ethers file for the test network looks like:

```
00:00:B7:B6:3D:F6      ALICE
00:50:DA:E4:61:34      RICHARD
00:00:C0:1A:AA:6E      RUPERT
```

(By convention, names for MAC addresses are entered in uppercase, so as not to confuse them with IP hostnames.) Now if we run "tcpdump -f -t -e" ("-f": show "foreign" addresses as numeric – prevents name lookups for external IP addresses) we get the much more readable trace:

```
ALICE RICHARD ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
RICHARD ALICE ip 70: 10.1.1.22 > 10.1.1.11: icmp redirect 128.9.0.107 to host 10.1.1.254
RICHARD RUPERT ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
ALICE RUPERT ip 98: 10.1.1.11 > 128.9.0.107: icmp: echo request
```

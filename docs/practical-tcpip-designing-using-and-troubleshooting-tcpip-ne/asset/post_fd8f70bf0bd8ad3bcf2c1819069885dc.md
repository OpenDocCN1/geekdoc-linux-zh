
![](img/a2132b646d336d5f9a21102d6320e537_638_0.png)

**Figure 23.7** Allocating addresses to your Internet router and your LAN

In the next Module we'll look at how to allocate addresses when we've finished testing and inserted our firewall into the network.

### 23.7 IP addressing for the live network

In the previous module we explained how to handle public/private addressing for the preliminary testing of your Internet connection. In this module we assume your connection has been tested and is working OK. You now have to insert your firewall into your network and configure your IP addressing for live running.

### 1. At least one public, static IP address

There are two variants here:

- i. many public, static IP addresses. You may choose to use NAT or not. If you do, the NATing will be performed by your firewall. (Typical examples: ADSL for business use, permanent leased line.)
- ii. a single, public, static IP address. If you want more than one machine on your LAN (and we assume you will), you must use NAT, performed by your firewall; otherwise, this is just a small instance of (i) above. (Typical examples: analog dial-up or ADSL for home use.)

![](img/a2132b646d336d5f9a21102d6320e537_639_0.png)

![](img/a2132b646d336d5f9a21102d6320e537_639_1.png)

**Figure 23.8** Allocating IP addresses to machines on your live LAN

All the machines use the static, public addresses during testing (1a, Figure 23.7). If you're not going to use NAT, adding the firewall (1b, Figure 23.8) is very easy because you continue to use the numbers from testing. If you do implement NAT, it becomes active only after you add your firewall, so you will have to renumber your test machines after the firewall is installed (1c, Figure 23.8). However, as we install only one or two machines for testing, this is a very small job.

If you have only one address, you will have to omit step K (Module 23.9 – adding extra machines) from your testing until you add a firewall (1c Figure 23.8). For reasons of space we won't treat this as a special case any more – it's just an instance of case (ii) with NAT.

If you chose (probably unwisely) not to implement a firewall, then your test configuration (1a or 2a) will be your final, live configuration too.

### 2. No static IP addresses

Because the machines on your LAN use NATed addresses during testing, there’s no need to change the addresses when you go live. Your Internet router almost certainly gives you the option to specify what the NATed, private address range is for your LAN, and may even be able to act as a DHCP server for internal machines. Choose a range of private addresses that you can configure in your Internet router, or use the router’s pre-configured range if you have to.

If you install a firewall later:

- you can allocate the firewall’s external address manually from the range of internal addresses your router is configured with. Alternatively, it may be able to get its external address by DHCP server from the router (2b, Figure 23.8).
- you can allocate the addresses to the LAN machines manually, or using a DHCP server – in the firewall if it has one, or else on the LAN.

Now that you know which IP addresses you’ll be using in the preliminary testing phase, we get started on constructing the network, in the next Module.

### 23.8 Implementation (1)

**A. Draw a sketch-map of your planned network**

Draw your network as you expect to implement it and add the IP numbers you expect to allocate. (See Appendix 9 for an example.)

**B. Allocate your IP addresses for testing**

By now you know the range of IP addresses (“LAN-IP-range”), and the netmask (“LAN-netmask”) you’ll be using on your LAN – either the static range your ISP allocated, or the NAT range you will configure on your router for in step C below.

| Item | Value |
|---|---|
| **LAN-IP-range** | . . . . |
| **LAN-netmask** | . . . . |
| **LAN-default gateway = IP address of router’s internal interface** | . . . . |

**C. Configure your router’s NAT settings if it’s performing NAT**

(This applies only if you have what we called connection type 2 in the previous module – no static IP addresses at all. If you will be using NAT but have static IP addresses, skip this step, because you use non-NATed addresses for the first phase of testing.)

You want to tell your router the range of IP numbers that you’ll be using on your private (internal) network. These are specified by the LAN-IP-range and LAN-netmask in step B above.

Most routers nowadays have a Web interface, and we’ve found that configuring NAT isn’t a big deal. With a modern device with a good user interface, it might take you less than half an hour, including finding and reading the relevant documentation. (With a bad user interface and bad documentation it could take you days.)

![](img/a2132b646d336d5f9a21102d6320e537_642_0.png)

**Figure 23.9** Cabling for preliminary testing of your Internet connection

**D. Install your cabling**

Nowadays this will almost certainly be 10/100Mbps UTP Ethernet, although gigabit Ethernet and wireless networking are becoming affordable and popular. Assuming you’re using UTP, for performance reasons you’d use a switch rather than a hub (c.f. Module 2.8 and Appendix 3), but to make network testing and debugging easy, a non-switched hub is much better. The best compromise is to buy a small hub, use it for your preliminary installation (Figure 23.9), and when everything is working replace it with a switch. You’ll need the hub later on anyway, for day-to-day testing and debugging as we described in Chapter 2. And, for tracing just the traffic to/from the Internet, you can insert the hub between the Internet router and the switch; this lets you see all Internet traffic but doesn’t slow down your LAN.

**E. Install a tcpdump diagnostic PC and a separate dial-up PC for testing**

We always make the mistake of thinking everything will work first time and forget this step. In fact things never work first time, so it’s much quicker to put your diagnostic tools in place right from the beginning; it saves you time and gives you great confidence when you can see exactly what’s happening on the wire.

- a. set up a PC running **tcpdump** (Figure 23.9). It doesn’t matter what its network settings are, because it’s only listening on the wire, never sending. (You can use this to impress your managers too. “Look, there’s our very first e-mail packet going out to the Internet.”)
- b. set up a stand-alone PC with a dial-up connection to the Internet. You will use this to test that your site can be accessed from the Internet. It’s best if the ISP you use for this dial-up is *not* the same one as you use for your main connection, so that your tests exercise more of the Internet. (If you use the same ISP for both, the connection from the ISP to the rest of Internet could be broken; you could still dial in and connect to your own main site, but not be able to connect to other sites, and you wouldn’t know why.)

### 23.9 Implementation (2)

**F. Install and test basic Internet connectivity on a single LAN PC**

At this point you only need to configure the three magic settings:

- i. static IP address: choose one from LAN-IP-range (from step B). Make sure you don't use the same address as your router. Even if you are going to use DHCP later on, allocate the IP address manually for this test, to reduce the number of variables
- ii. netmask = LAN-netmask (from step B)
- iii. default gateway = LAN-default-gateway (from step B).

Verify that you can:

- a. **ping** yourself, on both the loopback address (127.0.0.1) and the address you just configured on your PC
- b. **ping** the internal interface of the router
- c. **ping** a site on the Internet. (You have to specify an IP number, not a hostname, as you haven't configured DNS yet. Your ISP has probably given you the IP numbers of their DNS or mail servers: pick one of them to **ping** if you can't find any others easily. And remember that some sites don't allow **ping**. If in doubt, check using your stand-alone dial-up connection that the site you choose does respond to **pings**.)

Using your stand-alone dial-up PC, connect to the Internet. Now, from this dial-up PC:

- d. **ping** the test PC you've just installed on your LAN. (This won't be possible if you're using NAT without special configuration of your NAT system.)
- e. if the LAN PC is running any server (e.g. **daytime**, **telnet**, etc.) attempt to connect to that service
- f. if your ISP has set up DNS for you, use **nslookup** or **host** to check that the DNS entries you expect really are present. Let's assume your domain is **example.com** and your ISP has set up MX entries for mail servers for you, and also an entry for a Web server, your tests will be something like:

```
nslookup -q=mx example.com
nslookup www.example.com
```

If you're not using the ISP's DNS for your public server addresses (if you have any public servers), you'll have to defer these tests until step L or M.

If any of these tests fail, you will have to check out what's happening as we explained in Part 1; `tcpdump` will help you isolate where the problem lies.

**G. Configure the test PC for DNS, and test DNS operation**

Configure the PC on the LAN to use the DNS server(s) at your ISP, and test it using **ping** (or `nslookup` or `host`). For example:

```
ping www.uit.co.uk
ping www.debian.org
ping www.aw.com
```

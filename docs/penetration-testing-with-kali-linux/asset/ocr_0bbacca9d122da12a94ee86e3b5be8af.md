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

+   1. Understand what port forwarding is
2. Learn when to use port forwarding techniques

> ⁸⁰ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Deep_packet_inspection
⁸¹ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Port_forwarding
⁸² (Wikipedia, 2019), https://en.wikipedia.org/wiki/Tunneling_protocol
⁸³ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Encapsulation_(networking)
⁸⁴ (Wikipedia, 2022), https://en.wikipedia.org/wiki/Network_topology

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

564
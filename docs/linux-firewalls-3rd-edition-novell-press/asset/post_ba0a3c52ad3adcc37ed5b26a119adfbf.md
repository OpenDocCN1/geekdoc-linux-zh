
The server allocates a new socket on its end, (*web server IP address, 80*) and associates it with the client socket.

## **FIGURE 1.6**
A TCP client connection request.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_47_0.png)

The web server responds with an acknowledgment (*ACK*) to the *SYN* message, along with its own synchronization request (*SYN*), as shown in Figure 1.7. The connection is now half open.

## **FIGURE 1.7**
A TCP server connection request acknowledgment.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_47_1.png)

Two fields not visible to the packet-filtering level are included in the SYN-ACK header. Along with the ACK flag, the server includes the client’s sequence number incremented by the number of contiguous data bytes received. The purpose of the acknowledgment is to acknowledge the data the client referred to by its sequence number. The server acknowledges this by incrementing the client’s sequence number, effectively saying it received the data, and sequence number plus one is the next data byte the server expects to receive. The client is free to throw its copy of the original SYN message away now that the server has acknowledged receipt of it.

The server also sets the SYN flag in its first message. As with the client’s first message, the SYN flag is accompanied by a synchronization sequence number. The server is passing along its own starting sequence number for its half of the connection.

This first message is the only message the server will send with the SYN flag set. This and all subsequent messages have the ACK flag set. The presence of the ACK flag in all server messages, as compared to the lack of an ACK flag in the client’s first message, will be a critical difference when we get to the information available for constructing a firewall.

Your machine receives this message and replies with its own acknowledgment, after which the connection is established. Figure 1.8 shows a graphic representation of this. From here on, both the client and the server set the ACK flag. The SYN flag won’t be set again by either program.

## FIGURE 1.8

TCP connection establishment.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_48_0.png)

With each acknowledgment, the client and server programs increment their partner process's sequence number by the number of contiguous data received, plus one, indicating receipt of that many bytes of data, and indicating the next data byte in the stream the program expects to receive.

As your browser receives the web page, your machine receives data messages from the web server with packet headers, as shown in Figure 1.9.

## FIGURE 1.9
An ongoing TCP server-to-client connection.

![](img/d1359a287d9d43cd5ed19f3a7b55d40d_49_0.png)

## Summary

The simple examples in this chapter illustrate the information that IP packet-filtering firewalls are based on. Chapter 2, "Packet-Filtering Concepts," builds on this introduction, describing how the ICMP, UDP, and TCP message types and service port numbers are used to define a packet-filtering firewall.

## CHAPTER 2

### Packet-Filtering Concepts

What is a firewall? Over the years, the term has changed in meaning. According to RFC 2647, “Benchmarking Terminology for Firewall Performance,” a firewall is “a device or group of devices that enforces an access control policy between networks.” This definition is very broad, purposefully so in fact. A firewall can encompass many layers of the OSI model and may refer to a device that does packet filtering, performs packet inspection and filtering, implements a policy on an application at a higher layer, or does any of these and more.

A stateless firewall usually performs some packet filtering based solely on the IP layer (layer 3) of the OSI model, though sometimes higher-layer protocols are involved in this type of firewall. An example of this type of device might include a border router that sits at the edge of a network and implements one or more access lists to prevent various types of malicious traffic from entering the network. Some might argue that this type of device isn’t a firewall at all. However, it certainly appears to fit within the RFC definition.

A border router access list might implement many different policies depending on which interface the packet was received on. It’s typical to filter certain packets at the edge of the network connecting to the Internet. These packets are discussed later in this chapter.

As opposed to a stateless firewall, a stateful firewall is one that keeps track of the packets previously seen within a given session and applies the access policy to packets based on what has already been seen for the given connection. A stateful firewall implies the basic packet filtering capabilities of a stateless firewall as well. A stateful firewall will, for example, keep track of the stages of the TCP three-way handshake and reject packets that appear out of sequence for that handshake. Being connectionless, UDP is somewhat trickier to a stateful firewall because there’s no state to speak of. However, a stateful firewall tracks recent UDP exchanges to ensure that a packet that has been received relates to a recent outgoing packet.

An *Application-level gateway* (ALG), sometimes referred to an as *Application-layer gateway*, is yet another form of firewall. Unlike the stateless firewall, which has knowledge of the Network and possibly Transport layers, an ALG primarily handles layer 7, the Application layer of the OSI model. ALGs typically have deep knowledge of the application data being passed and can thus look for any deviation from the normal traffic for the application in question.

An ALG will typically reside in between the client and the real server and will, for all intents and purposes, mimic the behavior of the real server to the client. In effect, local traffic never leaves the LAN, and remote traffic never enters the LAN.

ALG sometimes also refers to a module, or piece of software that assists another firewall. Many firewalls come with an FTP ALG to support FTP's port mode data channel, where the client tells the server what local port to connect to so that it can open the data channel. The server initiates the incoming data channel connection (whereas, usually, the client initiates all connections). ALGs are frequently required to pass multimedia protocols through a firewall because multimedia sessions often use multiple connections initiated from both ends and generally use a combination of TCP and UDP together.

ALG is a proxy. Another form of proxy is a circuit-level proxy. Circuit-level proxies don't usually have application-specific knowledge; but they can enforce access and authorization policies, and they serve as termination points in what would otherwise be an end-to-end connection. SOCKS is an example of a circuit-level proxy. The proxy server acts as a termination point for both sides of the connection, but the server doesn't have any application-specific knowledge.

In each of these cases, the firewall's purpose is to enforce the access-control or security policies that you define. Security policies are essentially about access control—who is and is not allowed to perform which actions on the servers and networks under your control.

Though not necessarily specific to a firewall, firewalls many times find themselves performing additional tasks, some of which might include Network Address Translation (NAT), antivirus checking, event notification, URL filtering, user authentication, and Network-layer encryption.

This book covers the ideas behind a packet-filtering firewall, both static and dynamic, or stateless and stateful. Each of the approaches mentioned controls which services can be accessed and by whom. Each approach has its strengths and advantages based on the differing information available at the various OSI reference model layers.

Chapter 1, “Preliminary Concepts Underlying Packet-Filtering Firewalls,” introduced the concepts and information a firewall is based on. This chapter introduces how this information is used to implement firewall rules.

### A Packet-Filtering Firewall

At its most basic level, a packet-filtering firewall consists of a list of acceptance and denial rules. These rules explicitly define which packets will and will not be allowed through the network interface. The firewall rules use the packet header fields described in Chapter 1 to decide whether to forward a packet to its destination, to silently throw away the packet, or to block the packet and return an error condition to the sending machine. These rules can be based on a wide array of factors, including the source or destination IP addresses, the source and (more commonly) destination ports, portions of individual packets such as the TCP header flags, the types of protocol, the MAC address, and more.

MAC address filtering is not common on Internet-connected firewalls. Using MAC filtering, the firewall blocks or allows only certain MAC addresses. However, in all likelihood you only see one MAC address, the one from the router just upstream from your firewall. This means that every host on the Internet will appear to have the same MAC address as far as your firewall can see. A common error among new firewall administrators is to attempt to use MAC filtering on an Internet firewall.

Using a hybrid of the TCP/IP reference model, a packet-filtering firewall functions at the Network and Transport layers, as shown in Figure 2.1.

The overall idea is that you need to very carefully control what passes between the Internet and the machine that you have connected directly to the Internet. On the external interface to the Internet, you individually filter what’s coming in from the outside and what’s going out from the machine as exactly and explicitly as possible.

For a single-machine setup, it might be helpful to think of the network interface as an I/O pair. The firewall independently filters what comes in and what goes out through the interface. The input filtering and the output filtering can, and likely do, have completely different rules. When speaking of a Linux firewall, the lists of rules defining what can come in and what can go out are called *chains*. The I/O pair is the list of rules on the input chain and the list of rules on the output chain. The lists are called *chains* because a packet is matched against each rule in the list, one by one, until a match is found or the list is exhausted, as depicted in Figure 2.2.

# TCP

We’ve deliberately steered clear of most of the guts of TCP, and explained how it works using our postcards/packets analogy. This was acceptable on the basis of our “do you need to know this in your day-to-day work?” guiding principle. You *don’t* need to worry about the guts of TCP – it just works. What you do need is to be able to recognize when a TCP connection is being established and terminated, and what a RESET is when a connection is refused.

Surprisingly at first sight, not all applications need or use the reliability and connection-oriented features of TCP. In Chapter 15 we’ll see that several important applications use the UDP transport (host-to-host) layer protocol. While this is connectionless and only best-effort (“unreliable”), it is sometimes more appropriate than TCP.

*ping* doesn’t use UDP or TCP – it uses ICMP only. If you look at the processes running on a target machine you won’t see any **ping** server; it’s not needed because replying to **pings** is built into the TCP/IP stack, which is easily done because it’s so simple and small.

# Other features of TCP

Steve’s, Chapters 17–24 cover TCP and all its features in great detail. We’ll just mention two features here.

TCP supports “congestion control” – how the client and server can avoid saturating the network and making it unusable because there is too much traffic to be handled properly. The “old” way of doing this was for the systems to send *ICMP source quench* messages to each other, in effect saying “please send more slowly.” Nowadays this isn’t recommended; instead, if packets are coming too quickly, some of them are just dropped silently (i.e. without generating any ICMP messages) and the two ends of the connection “learn” – by seeing they have to retransmit frequently – that they should reduce their transmission rate. It is surprising that some of today’s sophisticated “bandwidth management” devices – which let you allocate, for example, 20% of your Internet connection’s bandwidth to incoming Web traffic, and 30% to VPNs between your offices, operate using what seems such a crude mechanism.

The other point we’ll mention is that some security systems actively generate TCP RSTs (resets). For example, if the security system detects that a user is accessing an unauthorized Web site, it sends a RST to the client on the LAN, with the IP source address faked to be that of the remote Web server, thus aborting the client’s connection to the unauthorized site.

TCP itself is a large and complex protocol, but because all the complexity is isolated in networking stack, you don’t see it at the application level so writing TCP applications is easy (relatively). You only have to worry about the application-specific code since the huge amounts of functionality in the TCP layer are provided free. This is an example of good software engineering.

# “Sockets,” ports, and connections

You will frequently come across references to “sockets” in TCP/IP documentation. The most common application programming interface (API) to TCP/IP is the *Sockets API*. This originated at Berkeley, in their 4.2BSD release of UNIX in 1983, and sockets are often referred to as “Berkeley sockets” or “BSD sockets.”

A socket is one end of a TCP connection. It is specified by the host IP address and the port number. To create a connection, the server creates a socket on its own address and its well-known port, and then listens on that socket. The client creates a socket on its own address and
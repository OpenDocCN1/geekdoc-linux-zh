# # Packets and Routers

What the browser wants to do is send a command to the Web server on Sunsite that looks like this:

```
GET /LPD/HOWTO/Fundamentals.html) HTTP/1.0
```

Here’s how that happens. The command is made into a *packet*, a block of bits like a telegram that is wrapped with three important things: the *source address* (the IP address of your machine), the *destination address* (152.19.254.81), and a *service number or port number* (80 in this case) that indicates that it’s a World Wide Web request.

Your machine then ships the packet down the wire (modem connection to your ISP, or local network) until it gets to a specialized machine called a router. The router has a map of the Internet in its memory—not always a complete one, but one that completely describes your network neighborhood and knows how to get to the routers for other neighborhoods on the Internet.

Your packet may pass through several routers on the way to its destination. Routers are smart. They watch how long it takes for other routers to acknowledge receipt of a packet. They use that information to direct traffic over fast links. They use it to notice when other routers (or a cable) have dropped off the network, and compensate if possible by finding another route.

There’s an urban legend that the Internet was designed to survive nuclear war. This is not true, but the Internet’s design is extremely good at getting reliable performance out of flaky hardware in an uncertain world. This is because its intelligence is distributed through thousands of routers rather than a few massive switches (like the phone network). This means that failures tend to be well localized and the network can route around them.

Once your packet gets to its destination machine, that machine uses the service number to feed the packet to the Web server. The Web server can tell where to reply to by looking at the command packet’s source IP address. When the Web server returns this document, it will be broken up into a number of packets. The size of the packets will vary according to the transmission media in the network and the type of service.

# ## TCP and IP

To understand how multiple-packet transmissions are handled, you need to know that the Internet actually uses two protocols, stacked one on top of the other.
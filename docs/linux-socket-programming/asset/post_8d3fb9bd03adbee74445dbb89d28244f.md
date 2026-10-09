
## Data Flow Glitches

Communication between peers is not always clear. Each may assume that the other is supposed to talk first (network deadlock). Another problem is like being placed on hold forever: You are never sure that the person hasn't put you on hold and taken a coffee break for the rest of the day.

Starvation occurs when a requestor waits indefinitely for a response. The cause may include a bad network, slow peer, rebooted peer, and so on. In most cases, you can solve a starved receiver by programming a tickler, which is simply a message to remind the sender that your receiver program is still waiting.

The tickler should wait a period of time before getting impatient. You could include the last sequence ID sent and even a time stamp in the message. After hearing nothing from the sender, the receiver may reset the connection. This process does require the sender to understand the tickler and connection reset messages.

A network deadlock can happen when one of the messages is lost during a packet interchange. The sender waits for the reply, while the receiver still waits for the lost message. Your tickler could help break the deadlock as well. For example, in the packet interchange example, the receiver tickles your sender with the last sequence ID it got. Your program, in turn, retransmits the lost message.

## Juggling Tasks: A Multitasking Introduction

Going back to the sender and receiver programs, why use two programs? Why not use just one? Using one program is possible, but when you want to send and receive at the same time, you essentially need two programs.

Suppose that you had a distributed program (a program that uses the network as a multiprocessor) that processes image data very quickly. Your network uses several stages to process the image: image capturer, deflecker, smoother, quantizer, and serializer. Each of these is on a different computer, and the information flows from one stage to the next. The smoother receives data from the deflecker, processes the information, and passes it on to the quantizer. Each middle stage must receive and send nearly at the same time, like a bucket with a hole in the bottom.

In this example, you cannot easily combine two stages. Each stage has to be separate, so that the information going in does not get muddied with the results going out. Of course you could toss in the issue of image error: How do you get an error message *up* the cascade?

Dividing the task into well-defined responsibilities is part of the concept of *multitasking*. You can run several programs at the same time in their own contexts to ensure that the inputs and outputs never mingle. This avoids corrupted results. The examples you see in this chapter use a form of multitasking because they run as separate programs.

The programs are actually similar enough that you could merge them into one so that they talk to themselves. In that case and to simplify the interactions, you must create a separately running task for each, indicating which one sends the first message.

Multitasking is integrally embedded in network programming. [Chapter 8, "Choosing when to Wait for I/O."] discusses multitasking in greater detail.

## Summary: Connected Versus Connectionless Models

Passing messages between peers or clients and servers involves either connection-based or connectionless communication. With connection-based messages, you can simply open a channel, connect to a peer, and proceed to send and receive information. The connection keeps track of your destination for you, so you don't have to restate it. Both TCP and UDP support a connection; however, only TCP encompasses connection with reliability and ordering. UDP's connection offers a mere shorthand, so you can use higher I/O services than sendto() and recvfrom().

Connectionless message passing is similar to mailing a letter: You need to address each message before sending. To do this, you must use calls other than send() and recv() that the connection-based communication uses. These are sendto() and recvfrom(). These system calls mirror the other calls but add destination and source addresses.

Transaction TCP (T/TCP) is essentially a connectionless TCP. If supported (Linux does not yet support T/TCP), T/TCP helps you to avoid the lengthy setup and shutdown times. This speeds transmission of your messages. Also, the abbreviated protocol focuses on the packet instead of the stream and reduces interaction to three message packets.

By default UDP is connectionless, but you may connect the UDP socket to ease programming. Unlike TCP, you can reconnect the same socket to different peers.

TCP provides you reliability but also carries a load of overhead. You can add reliability to UDP one piece at a time by ensuring data arrival, sequencing packets, eliminating redundancy, verifying data integrity, and removing data flow problems. TCP and UDP provide different levels of reliability and interaction. TCP lets you view the information like a stream; UDP gives your program access to the individual messages. Each of these builds on IP's architecture, functionality, and model.

# Chapter 5. Understanding the Network Layering Model

IN THIS CHAPTER

- *Solving the Network Challenge*
- *Open Systems Interconnection (OSI) Network Model*
- *Internet Protocol Suite*
- *Fundamental Differences Between OSI and IP*
- *What Services What?*
- *Summary: From Theory to Application*

One of the most delicious European desserts is the torte, a kind of very rich cake. The torte typically has several (five to eight) layers. Each layer rests its weight on the lower layers and has a different flavor and color. The torte has a firm frosting that covers the crest to the platter.

If you look at how the conceptual network subsystem (or *protocol stacks*) is designed, you find a similar layering. On the surface it shows a common interface with the layers underneath. Each layer of the network rests on top of another to support its features. This dependence is very important: If any part of the lower layers fails, the whole subsystem either crashes or functions less optimally.

Partitioning the network responsibilities provides the support for the weighty features of higher-level functions. The network subsystem is a large and complicated mix of hardware, memory, security, data, kernel, and application. Coordinating all these technologies is the network challenge.

All too frequently, unless you really understand the synergy of the technologies, coordinating their fusion burdens the network challenge.

Network modeling addresses the network challenge without losing portability. This chapter introduces the network challenge and presents two models that attempt to solve it.

## Solving the Network Challenge

Network programming involves so many parts of computer science and software engineering that working at a low level is very complicated. Similar to building a house, if you focus on cutting the timber, you may never complete the house. But, by combining the proper tools and materials, you can think more about your finished product and the potential features.

The challenges network programming introduces are what makes this particular technology so interesting. However, to program the network from the ground up, you must be a guru (or master of all computer trades). The challenges of network programming include hardware, transmission, operating system interfacing, and program interfacing.

## Networking Hardware Issues

Technology provides many options for implementing a network. The options include conducted versus nonconducted media (some physical conduit to carry the signal), electrical versus nonelectrical transmission, directed versus undirected paths, and short versus long distance. Table 5.1 lists a few forms of network connections.

Table 5.1. Network Media Have Different Characteristics and Limitations

| Media | Conducted | Electrical | Directed | Distance | Top Throughput |
|---|---|---|---|---|---|
| Coaxial cable | yes | yes | connected | <2Km | 10Mb/s |
| Twisted pair | yes | yes | connected | <150m | 100Mb/s |
| Fiber optic | yes | no | connected | (unlimited) | 100Gb/s |
| Wireless: HF | no | yes | broadcast | >1000Km | <10Kb/s |
| Wireless: VHF/UHF | no | yes | broadcast, line of sight | <30Km | <40Kb/s |
| Wireless: microwave | no | yes | yes, line of sight | <30Km | <1Mb/s |
| Satellite | no | yes | yes | (unlimited) | <10Mb/s |
| Infrared | no | no | yes, broadcast | <10m | <1Mb/s |
| Laser | no | no | yes | very long | <100Gb/s |

Fortunately, the kernel hides all these technologies from your direct interaction. Imagine how difficult it would be to know what kind of medium and transmission the computers use. Yet all of these technologies have to deal with several common problems.

One problem with many technologies is *signal attenuation*, or line loss, from media resistance. Electrical types of transmission are particularly susceptible to this problem. The message may degrade from the medium itself. Line signal loss is a real problem for certain technologies (for example, twisted pair and coaxial cabling). The physics of electric and radio transmission attenuate your message as it passes through the medium.

Another problem is *collisions*. Several computers sharing the same medium (conducted or nonconducted) may cause collisions where they transmit messages at the same time. If your computer sends a packet while another is being transmitted, the resulting collision garbles both packets. The two computers must detect collisions, back off, recover, and retransmit.

# TCP/IP and Linux Protocol Implementation

Of course there is a little bit of hardware involved, as well as people using the system. The important point is that most of the hardware components are general-purpose programmable computers, and as such, we have all the flexibility that such devices enjoy. Of particular relevance to this book is the fact that the performance of the hardware in the form of personal computers running off-the-shelf operating systems such as Linux is now sufficient to fulfill most of the important roles in the Internet.

What are the main components of the Internet? We can look at them from many viewpoints, but from 20,000 feet they might be the following:

+   **Users.** Users are either people, or their agents, that access content over the Internet using networked applications to download Web pages or move email or run VoIP.

+   **Content.** In the end, users content—whether it is to access a Web page, acquire a real-world good or service, or hear the voice of their friend.

+   **Service providers.** Service providers are organizations to which users subscribe (have some contract-like relationship with) that manage connectivity by acquiring lower-level services and coordinating them. Service providers may provide content, applications, or Internet connectivity. This space is constantly expanding as more and more layers of business are refined out of the global information market. Traditionally, Internet service providers (ISPs) bought bit-transport capacity, and added value by managing a collection of links and routers. More recently at least two layers have been added, with content and application service offering overlay services, with collections of coordinated, managed end systems connected to one or more ISPs offering optimized performance for this set of users or others.

+   **Hosts, or end systems.** End systems are hosts (general-purpose computers) that run client, server, or peer-to-peer application software. The term has become somewhat muddied in recent years due to the emergence of the other business layers, and also due to some hacks required to make security and addressing deploy pragmatically (see Chapter 10 for some details on). Thus we have seen the evolution of middle boxes, which provide a variety of services ranging from proxying, caching, firewalls, address translation, and so on. Pure end systems use users (i.e., clients, servers, or peers).

+   **Middle boxes.** Middle boxes are end systems that do not have explicit users (clients or servers) attached, but intermediate at the application, transport, or network level in the protocol stream to provide some kind of added-value service or optimization.

+   **Intermediate systems, or routers.** Intermediate systems that provide a router (or as it it used to be commonly known, IP gateway) service are,
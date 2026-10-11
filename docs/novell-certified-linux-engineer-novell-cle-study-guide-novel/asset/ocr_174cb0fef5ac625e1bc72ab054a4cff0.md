# ## Advertising Services with SAP

Early on, eDirectory didn't run on Windows or Linux servers. The only plat-form it ran on was Novell NetWare:

> **TIP.** **The first versions of eDirectory were named Novell Directory Services (NDS).**

Back then, NetWare didn't natively support the TCP/IP protocol. You had to use the Internetwork Packet Exchange (IPX) protocol instead. IPX was a very easy-to-use protocol; essentially, all you had to do was plug your server or workstation into the network jack, and the protocol would automatically configure itself. You didn't need DHCP to dynamically assign addresses. You also didn't need a DNS server to resolve hostnames into network addresses. That's because IPX used (and still does) the Service Advertisement Protocol (SAP).

When an IPX server was booted, all the services it provided, such as file, print, and directory services, used the SAP protocol to advertise their avail- ability. Regardless of whether anyone wanted to use them, they would peri- odically send out broadcasts to the entire network describing the service they had to offer as well as their network address. If a service were to be shut down, it would stop advertising itself.

By way of analogy, imagine that you're sitting in a classroom taking a class. At 60-second intervals, each student in the class stands up and announces his or her name and the desk he or she is currently sitting in and then sits back down. Essentially, this is how SAP works.

This strategy works very well, and if you've ever used Novell's Client software on a Windows workstation to log in to an IPX server, you know that you can browse the network to select the eDirectory tree and server you want to log in to. The Novell Client generates the list of trees and servers by simply lis- tening on the network wire for SAP broadcasts, as shown in Figure 5.2.

![](bbox=[0.04, 0.77, 0.17, 0.82])
# ### 17.13 NTP – Network Time Protocol

NTP (the *Network Time Protocol*) keeps computer clocks synchronized with each other. You can use it to:

+   - make sure all the computers on your network show the same time
+   - make sure they are all showing the *correct* time, by synchronizing them with an accurate, external reference server.

Keeping accurate time throughout your site is a good idea for many reasons:

+   - you can accurately correlate events in different log files on different machines, e.g. if you suspect a security breach and want to check a sequence of actions across your site
+   - file backup applications need to know when a file has changed, to decide whether it needs to be backed up
+   - when you use networked file systems, such as NFS (in the next module) or Microsoft Windows Networking (Part 3), there are at least two potentially different clocks involved – one on the client and one on the server. If the server is ahead of the client, a file could appear to have been modified some time in the future
+   - network performance monitoring – how long does each hop take as a packet is routed across the network?
+   - caches of Web pages use the current time to decide whether a page in the cache is up to date and may be used, or is out of date and must be retrieved again.

Real-world applications, such as air-traffic control, process control in factories, and financial trading where, for example, stock prices are changing with time, obviously need accurate time-keeping too.

NTP works by noting the time it takes for packets to travel between client and server, and estimating the error involved:

![](bbox=[0.27, 0.66, 0.73, 0.72])

The client sends an NTP message to the server; the time according to the client’s clock (T_c) is 520. The server receives the message, and records when it arrived, according to its own clock (T_s = 700). The server processes the packet and responds, giving both its current time (T_s = 730) and when it received the packet (T_s = 700). This message arrives at the client at T_c = 590. The total round trip time is (590 – 520) = 70. However, the server had the packet for (730 – 700) = 30, so the network-only round trip time is (70 – 30) = 40. Therefore, the approximate time for a single trip from server to client is 40/2 = 20. Therefore, the message that arrived at T_c = 590 was sent by the server at T_c = (590 – 20) = 570. This means T_c 570 is the same as T_s 730, i.e. the client’s time is slow by (730 – 570) = 160 units. NTP on the client adjusts the clock to correct this. By default, small time adjustments – less than half a
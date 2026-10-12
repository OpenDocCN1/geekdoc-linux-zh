
Figure 0.2 is the **tcpdump** trace of this interaction with **tcpdump**, running on a third machine, Carol. Don’t worry about the detail here – we’ll cover every aspect of all this later on. For now, just notice that the trace illustrates the factors above – that we can see easily all the network traffic, and that what the user thinks of as a single TCP/IP networking activity really consists of several small pieces.

```
carol# tcpdump -n -t

arp who-has 192.0.2.19 tell 192.0.2.7
arp reply 192.0.2.19 is-at 00:c0:c0:8b:c3:c5
192.0.2.7:2205 > 192.0.2.19.53: 1+ A? bob.ui.co.uk. (32)
192.0.2.19.53 > 192.0.2.7.2205: 1 1/2/2 A 192.0.2.5 (131)
arp who-has 192.0.2.5 tell 192.0.2.7
arp reply 192.0.2.5 is-at 80:0:20:c:e4:e1
192.0.2.7 > 192.0.2.5: icmp: echo request
192.0.2.5 > 192.0.2.7: icmp: echo reply
```

**Figure 0.2 The tcpdump trace of Alice pinging Bob**

This looks agonizingly detailed just to **ping** a machine to see whether it’s alive, and indeed it is, in a way. But on the plus side, most of the same steps apply even if we’re dealing with a much more complex activity such as browsing to a Web page, and that lets us use **ping** as a simple but powerful diagnostic tool. And, because the individual steps in the conversation are well defined and separate, if anything goes wrong we can zero in on the cause, which will be *specific to that step* and quickly fix the network.

The essence of our approach to building and maintaining networks is: don’t try to guess what’s happening – look at it on the wire instead, so you *know* what’s happening. Sniffers are an essential tool. Don’t think using one is a badge of ignorance – the opposite is true: you’ll find it’s the network gurus who use them all the time.

Working without a sniffer is like trying to diagnose what’s wrong with a car engine just by sitting in the back seat: you simply do not have all the information you need. Without a sniffer, what does a failed **ping** command tell you? Alice could be wrongly configured, or maybe Bob’s network card is broken, or the network cabling itself could have a problem; the symptoms are the same if you are using **ping** on its own. But when you combine it with the sniffer, **ping** is transformed into a high-resolution, low-granularity diagnostic tool – it lets you see every little bit if you want to. **tcpdump** lets you quickly rule out possible causes and concentrate on the areas where the problem really lies. We’ll show you many examples of this throughout the book. Using **tcpdump** is easy and it will soon become second nature to you.

## 0.2 Networks can be easier than stand-alone machines

On a network all communication to and from your machine passes a single point – the network card (or network interface card, or NIC). Therefore that’s the place to look to see what’s happening. Run `tcpdump` and it looks at all the traffic entering or leaving on that NIC, giving you a great view of the network activity (Figure 0.3).

![](img/a2132b646d336d5f9a21102d6320e537_35_0.png)

**Figure 0.3** `tcpdump` looks at all the traffic entering or leaving on the NIC

Network traffic for different applications is often addressed to different machines. For example, your machine connects to **www.microsoft.com** to browse a Web page, but it connects to a different machine, **mailserv.example.com** say, to collect your e-mail. That makes it easy to specify the traffic from the particular application or to the particular machine that you’re really interested in, and `tcpdump` has special options to let you filter out only what you specify (Figure 0.4). We’ll have countless `tcpdump` examples throughout the book but Figure 0.5 illustrates a simple case – look at traffic to and from host 192.0.2.29 only. Again, don’t worry about the detail for now – just note that every line shown is either sent from or received by the specified machine. (We truncated very long lines in the output to fit the page.)

![](img/a2132b646d336d5f9a21102d6320e537_35_1.png)

**Figure 0.4** The filter option in `tcpdump`

Analyzing an application’s network traffic can be much easier than trying to find out what the application is doing in memory and on disk when it runs on a stand-alone machine. Here’s a real example. We use a customer database in-house, and it runs slowly. When it ran stand-alone on a dedicated machine, we didn’t know what was happening. We then ran it using shared disk drives over the network, and looked at the network traffic using `tcpdump`. It showed that creating a new empty record involved between 100 and 300 writes to disk, each of about 145 bytes. We concluded that for the amount of data we had, this particular product wasn’t suitable and did not scale up to the size we needed. By contrast, getting the same format was much easier with the network version.

```
alice# tcpdump -n -t host 192.0.2.29
tcpdump: listening on eth0
192.0.2.17 > 192.0.2.29: icmp: echo request
arp who-has 192.0.2.17 (ff:ff:ff:ff:ff:ff) tell 192.0.2.29
arp reply 192.0.2.17 is-at 0:d0:b7:bb:3d:f6
192.0.2.29 > 192.0.2.17: icmp: echo reply
arp who-has 192.0.2.1 (ff:ff:ff:ff:ff:ff) tell 192.0.2.29
arp reply 192.0.2.1 is-at a0:50:73:38:c0:26
192.0.2.5.2581 > 192.0.2.29.25: S 1639808000:1639808000(0) win 4096 <mss 1460>
arp who-has 192.0.2.5 (ff:ff:ff:ff:ff:ff) tell 192.0.2.29
arp reply 192.0.2.5 is-at 8:0:20:c:e4:d1
192.0.2.29.25 > 192.0.2.5.2581: S 42686545970:42686545970(0) ack 1639808001 win 8760 <mss 1460> [DF]
192.0.2.29.25 > 192.0.2.29.25: . ack 1 win 4096
192.0.2.29.25 > 192.0.2.5.2581: P 1:131(130) ack 1 win 8760 [DF]
192.0.2.5.2581 > 192.0.2.29.25: P 1:22(21) ack 131 win 4096

192.0.2.29.58561 > 64.4.49.199.25: S 42686659970:42686659970(0) win 8760 <mss 1460> [DF]
64.4.49.199.25 > 192.0.2.29.58561: S 1574539292:1574539292(0) ack 42686659971 win 64240 <mss 1460> [DF]
192.0.2.29.58561 > 64.4.49.199.25: . ack 1 win 8760 [DF]
64.4.49.199.25 > 192.0.2.29.58561: P 1:101(100) ack 1 win 64240 [DF]
192.0.2.29.58561 > 64.4.49.199.25: P 1:22(21) ack 101 win 8760 [DF]
64.4.49.199.25 > 192.0.2.29.58561: . ack 22 win 64240 [DF]
64.4.49.199.25 > 192.0.2.29.58561: P 101:156(55) ack 22 win 64240 [DF]
192.0.2.29.58561 > 64.4.49.199.25: . ack 156 win 8760 [DF]
192.0.2.29.58561 > 64.4.49.199.25: P 22:63(41) ack 156 win 8760 [DF]
64.4.49.199.25 > 192.0.2.29.58561: P 156:199(43) ack 63 win 64240 [DF]
192.0.2.29.58561 > 64.4.49.199.25: P 63:94(31) ack 199 win 8760 [DF]
64.4.49.199.25 > 192.0.2.29.58561: P 199:242(43) ack 94 win 64240 [DF]
192.0.2.29.58561 > 64.4.49.199.25: P 94:100(6) ack 242 win 8760 [DF]
64.4.49.199.25 > 192.0.2.29.58561: P 242:88(46) ack 100 win 64240 [DF]
192.0.2.29.58561 > 64.4.49.199.25: P 100:801(701) ack 288 win 8760 [DF]
arp who-has 192.0.2.29 tell 192.0.2.19
192.0.2.19 > 192.0.2.29 is-at 8:0:20:a:74:aa

64.4.17.63.4992 > 192.0.2.29.25: S 26868585848:26868585848(0) win 16384 <mss 1460, nop, nop, sackOK>
192.0.2.29.25 > 64.4.17.63.4992: S 42755179770:42755179770(0) ack 26868585849 win 8760 <mss 1460> [DF]
64.4.17.63.4992 > 192.0.2.29.25: . ack 1 win 8760
192.0.2.29.25 > 64.4.17.63.4992: P 1:131(130) ack 1 win 8760 [DF]
192.0.2.29.25 > 64.4.17.63.4992: P 1:131(130) ack 1 win 8760 [DF]
64.4.17.63.4992 > 192.0.2.29.25: P 1:19(18) ack 131 win 17390
64.4.17.63.4992 > 192.0.2.29.25: . ack 131 win 17390
192.0.2.29.25 > 64.4.17.63.4992: P 131:215(84) ack 19 win 8760 [DF]
```

**Figure 0.5 Looking at traffic to and from 192.0.2.29**

Information on a stand-alone machine is much more difficult. We don’t have the source-code for the application, so we can’t add any debugging or tracing code. We’re not database experts, so we can’t trace the disk activity and relate it to whatever processes the application has started and how they interact with the operating system. But looking at the network traffic using **tcpdump** is child’s play.

This is like trying to understand how people carry out a complex mental computation. If one person does it on their own (a “stand-alone” computer), all you get is the answer; if it’s wrong, you don’t know why. If several people work on it together (a “network” of people), they talk to each other and ask each other questions. You can overhear what they are saying, so you can understand much more of the process involved in finding the answer.

We use **tcpdump** on our own network every day. We use it for many different purposes, not just network diagnostics, e.g. if the flickering lights on some of our network equipment show an abnormal, sustained level of network traffic coming from our Internet connection, it’s much quicker to run **tcpdump** to see what’s happening than to check through all the different logs on all the different servers. If it still looks weird, we can focus in on the offending application (or user).

In the next module, we see how the modular, building-block nature of TCP/IP helps you understand and troubleshoot your network.

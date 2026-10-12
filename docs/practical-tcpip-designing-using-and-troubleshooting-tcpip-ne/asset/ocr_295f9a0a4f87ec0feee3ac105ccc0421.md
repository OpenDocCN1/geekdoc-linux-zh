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

# **Figure 0.2 The tcpdump trace of Alice pinging Bob**

This looks agonizingly detailed just to **ping** a machine to see whether it’s alive, and indeed it is, in a way. But on the plus side, most of the same steps apply even if we’re dealing with a much more complex activity such as browsing to a Web page, and that lets us use **ping** as a simple but powerful diagnostic tool. And, because the individual steps in the conversation are well defined and separate, if anything goes wrong we can zero in on the cause, which will be *specific to that step* and quickly fix the network.

The essence of our approach to building and maintaining networks is: don’t try to guess what’s happening – look at it on the wire instead, so you *know* what’s happening. Sniffers are an essential tool. Don’t think using one is a badge of ignorance – the opposite is true: you’ll find it’s the network gurus who use them all the time.

Working without a sniffer is like trying to diagnose what’s wrong with a car engine just by sitting in the back seat: you simply do not have all the information you need. Without a sniffer, what does a failed **ping** command tell you? Alice could be wrongly configured, or maybe Bob’s network card is broken, or the network cabling itself could have a problem; the symptoms are the same if you are using **ping** on its own. But when you combine it with the sniffer, **ping** is transformed into a high-resolution, low-granularity diagnostic tool – it lets you see every little bit if you want to. **tcpdump** lets you quickly rule out possible causes and concentrate on the areas where the problem really lies. We’ll show you many examples of this throughout the book. Using **tcpdump** is easy and it will soon become second nature to you.
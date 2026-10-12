
An analogy is a crowded office: Alice wants to phone Bob but doesn't know his extension. A simple solution is for Alice to shout to the whole office, “Bob: I'm on extension 29. What's your extension?” Bob hears this and calls Alice back on extension 29, saying, “Alice, I'm on extension 7.” Then they can converse as much as they like without affecting other people with their shouting.

TCP/IP does something very similar, using ARP. Let's say Alice's machine is 192.0.2.7, and she wants to send to Bob's machine, 192.0.2.29. Machine .7 must find out .29's MAC address:

- Alice sends an Ethernet broadcast, containing an ARP request packet in the payload/data field. The ARP packet contains the IP address whose MAC address she needs - 192.0.2.29. **tcpdump** shows this as “arp who-has 192.0.2.29”
- all the machines on this wire receive this packet, extract the ARP packet, and look at the IP address inside it. If the address doesn't match the receiving machine's IP address, the packet is ignored, i.e. only .29 processes it further
- machine .29 replies to .7 with an ARP reply packet, containing .29's MAC address. (It does **not** broadcast the reply, because only .7 has asked for the information.) **tcpdump** shows this as “arp reply 192.0.2.29 is-at a.b.c.d.e.f.”
- .7 now knows .29's MAC address, and can communicate freely.

When we first met ARP, it looked like magic: how can two machines exchange over a network their addresses, when they need to be able to communicate with each other over the network? It seems circular. The key of course is using the broadcast. The Ethernet broadcast address is pre-defined so all machines know what it is and can use it without having to talk to any other machine first.

Below is the **tcpdump** trace of 192.0.2.7 pinging 192.0.2.29. We use options “-e”, to show the Ethernet addresses. We also use a new feature – specifying particular protocols as part of the filter expression. In this case, we want both ARP and ICMP (ping) traffic.

![](img/a2132b646d336d5f9a21102d6320e537_64_0.png)

Notice that there is only one ARP dialogue: .29 has sent a ping reply without issuing an ARP to find out .7's MAC address. .29 was able to do this because when it received the initial ARP request broadcast from .7, it extracted .7's MAC and IP addresses from the packet. It therefore didn't need to do its own ARP request afterwards – it already had all the information it needed to talk to .7.

> **Tip:** when I'm talking to you, my system uses ARP only when it thinks your machine is on the same wire. If you see an ARP “who-has” for a machine that you know is remote, it means your machine has an incorrect view of what the local network is: either its IP address, or more likely its netmask, is wrong.

## 2.5 Viewing and manipulating ARP entries

TCP/IP keeps a record of (IP address, MAC address) pairs in its *ARP cache*. It is only a cache and not a permanent store: once an entry reaches a certain age, TCP/IP deletes it. This stops the cache growing forever, and gets over the problem of how to detect whether the MAC address changes for a given IP address (e.g. if you have to replace a broken network card). On the other hand, it means the ARP dialog is repeated every so often, getting the same answer each time. (However, the load this imposes on the network is negligible.)

The arp command lets you view and manipulate the ARP cache (see Table 2.1).

### Table 2.1

| | Linux | Windows-NT |
|---|---|---|
| view the cache | arp<br>arp *host*<br>arp -a<br>arp -a *host* | arp -a<br>arp -a *ipnum* |
| **show addresses as numbers instead of names** | ... -n ... | |
| **delete an entry** | arp -d *host* | **arp -d *ipnum*** |
| **add ("set") an entry** | **arp -s *host macaddr*** | **arp -s *ipnum macaddr*** |

### Notes:

- 1. on Linux, arp by default prints host addresses as names and numbers ("**arp -a**") or just names ("**arp**"). As usual this works correctly only if you have DNS configured, which we don't cover until Chapter 7. Use option "-n" to prevent arp trying to convert the IP numbers to names
- 2. on Linux, the "-a" format display (Figure 2.8a) is slightly different to the one without "-a". We always use "-a", because it works on both Linux (Figure 2.8b) and NT (Figure 2.8c)
- 3. on Linux, *host* can be either an IP number or a hostname; on Windows you can use only IP numbers. See your manpages for more detailed descriptions
- 4. we've never needed to add entries, so you're unlikely to need to use "**arp -s**"
- 5. On Windows-NT, by default entries are deleted from the ARP cache after two minutes if they are not used, or ten minutes if they are used; the timeout period can be edited in the Registry, although it's hard to see why you would ever want to do that. On Linux, entries are usually deleted after about five minutes. (You can check the details of your implementation by ensuring an entry for a machine is present by pinging it, then running "**arp -a**" at intervals, to see when the entry vanishes.)

```
alice% arp -a -n
? (192.0.2.5) at 08:00:20:0C:E4:E1 [ether] on eth0
? (192.0.2.7) at 00:D0:B7:7F:A6:D9 [ether] on eth0
? (192.0.2.10) at 00:A0:C9:B4:E4:3A [ether] on eth0
? (192.0.2.22) at 00:02:B3:2A:49:1C [ether] on eth0
? (192.0.2.19) at 00:00:C0:8B:C3:C5 [ether] on eth0
alice%
```

(a)

```
alice% arp -a
mars.uit.co.uk (192.0.2.5) at 08:00:20:0C:E4:E1 [ether] on eth0
techpc.uit.co.uk (192.0.2.7) at 00:D0:B7:7F:A6:D9 [ether] on eth0
scutter.uit.co.uk (192.0.2.10) at 00:A0:C9:B4:E4:3A [ether] on eth0
denrisnt.uit.co.uk (192.0.2.22) at 00:02:B3:2A:49:1C [ether] on eth0
lee.uit.co.uk (192.0.2.19) at 00:00:C0:8B:C3:C5 [ether] on eth0
mail.uit.co.uk (192.0.2.29) at 08:00:20:0A:74:AA [ether] on eth0
alice%
```

(b)

```
C:\arp -a

Interface: 192.0.2.21 on Interface 2
Internet Address      Physical Address      Type
192.0.2.7             00-d0-b7-7f-a6-d9    dynamic
192.0.2.10            00-a0-c9-b4-e4-3a    dynamic
192.0.2.17            00-d0-b7-b6-3d-f6    dynamic
192.0.2.29            08-00-20-0a-74-aa    dynamic
C:\
```

(c)

Figure 2.8 “arp -a” outputs

(By the way, ARP is an example of a protocol that doesn’t sit neatly in the layer model. It’s really at layer 2${}_{\frac{1}{2}}$, linking the network or Internet or IP layer with the lower network access or link layer, as shown below.)

![](img/a2132b646d336d5f9a21102d6320e537_66_0.png)

We’ve used **ping** several times in this chapter and the previous one to generate some traffic, but we haven’t looked at it in detail. We’ll do that in the next module.

## 2.6 Using ping to generate test traffic between two machines

The **ping** program sends a special packet from my machine to yours. If your machine is connected to the network and receives the packet, it sends a reply to me saying you are alive. This is often just to check that a machine is alive, or just to generate test traffic between two machines.

**Ping** gets its name by analogy with sonar, where a submarine sends out small pulses of sound. The pulses echo back from other submarines and make a **ping** noise on the first submarine’s detector, indicating the presence of the other sub.

At its simplest, tell **ping** the IP address of the remote host you want to contact:

```
ping 192.0.2.29
```

The program sends multiple requests, and (hopefully) receives multiple replies. On Windows, the simple command `"ping host"` sends four requests and terminates, whereas on Linux it repeats forever (in fact until you press ctrl-C to terminate it). (There is no **ping** server on the target machine. Responding to **pings** is built into the TCP/IP stack, because it’s necessary for testing, and it’s so simple and small.) Bob shows **ping**’s output on Linux; we used option “-n” to print addresses as numbers, and “-c3” to send three requests.

```
alice# ping -c3 -n 192.0.2.29
PING 192.0.2.29 (192.0.2.29): 56 data bytes
64 bytes from 192.0.2.29: icmp_seq=0 ttl=255 time=4.5 ms
64 bytes from 192.0.2.29: icmp_seq=1 ttl=255 time=0.6 ms
64 bytes from 192.0.2.29: icmp_seq=2 ttl=255 time=0.5 ms
```

We can analyze this in detail using **tcpdump**, with option “-n” as usual (with extra lines inserted for clarity):

```
alice# tcpdump -n arp or icmp

15:05:53.170364 arp who-has 192.0.2.29 tell 192.0.2.17
15:05:53.171368 arp reply 192.0.2.29 is-at 8:0:20:a:74:aa

15:05:53.171384 192.0.2.17 > 192.0.2.29: icmp: echo request
15:05:53.174843 192.0.2.29 > 192.0.2.17: icmp: echo reply (DF)

15:05:54.168674 192.0.2.17 > 192.0.2.29: icmp: echo request
15:05:54.169217 192.0.2.29 > 192.0.2.17: icmp: echo reply (DF)
```

- Lines 1, 2: the usual ARP dialog. We wouldn’t see this if the target machine was on a remote network, or even if it’s on the LAN but we had been talking to it recently. The ARP often causes the first **ping** response time to be slower than the rest
- Lines 3, 4: the ARP dialog is followed immediately (16 microseconds) by the first **ping** request/reply pair
- Lines 5, 6: the next **ping** request/reply pair (etc.).

You can observe several points from the outputs of the two programs:

- 1. **ping** uses ICMP (the Internet Control Message Protocol), which is part of the TCP/IP suite of protocols. We will see a few other uses of ICMP elsewhere in the book

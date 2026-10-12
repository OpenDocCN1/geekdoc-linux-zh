
Now let’s see how this works in practice, when Alice pings Bob, i.e. she says “ping 192.168.0.86:”

- Alice’s TCP/IP routes the ICMP **ping** packet travels to her default gateway, 10.4.4.42, because the destination is outside her directly connected local network
- The VPN system in 10.4.4.42 (box A) inspects the destination address, 192.168.0.86, sees that it’s in the SPD, and therefore applies the specified SA for this address range:
    - The SA for this range is **A-to-B**
    - Box A encrypts and authenticates the **ping** packet with the keys from **A-to-B**, i.e. encrypts with 1111111111111111 and authenticates with key 2222222222222222
    - It creates a new packet with this encrypted/authenticated data as the payload, inserts the specified SPI (5001), and sets the destination address to the security gateway specified in **A-to-B**, i.e. 1.2.3.87. The source address of this packet is box A, not Alice, because Alice is hidden behind Box A. The final packet is shown simplistically below.

| src IP | dst IP | proto | SPI | encrypted payload |
| :--- | :--- | :--- | :--- | :--- |
| 192.0.2.42 | 1.2.3.87 | (VPN) | 5001 | encrypted payload |

- Box A’s TCP/IP routes this packet to its destination address, 1.2.3.87
- Now box B receives this packet. It sees that it’s a VPN packet and extracts the SPI, 5001
- It looks up SPI=5001 in its table of SAs, and finds it in the SA named **here-to-A**
- **here-to-A** says this packet should be decrypted with key 1111111111111111 and authenticated with key 2222222222222222, so box B performs these actions
- The packet is now restored to what it was as it left Alice, i.e. as shown below:

| src IP | dst IP | proto | payload |
| :--- | :--- | :--- | :--- |
| 10.4.4.41 | 192.168.0.86 | ICMP | **ping request** |

- Box B’s TCP/IP routes this normal, unencrypted packet to its destination address, which is 192.168.0.86, i.e. to Bob
- Bob receives the **ping** request, and sends a **ping** reply to the sender’s address, 10.4.4.41. Bob’s TCP/IP routes this to his default gateway, because the destination isn’t on his local, directly connected network. His default gateway is 192.168.0.87, i.e. box B – his site’s VPN system
- Box B then repeats all the steps that box A went through, so the **ping** reply is encrypted, sent to box A, decrypted, and finally forward to Alice, who is now happy because Bob replied to her **ping**.

Note that even though both Alice’s and Bob’s sites are using NAT, packets that travel through the VPN tunnel do *not* have their source/destination addresses translated: the whole packet is encrypted, and then decrypted, but otherwise unchanged. This fact is sometimes used to allow otherwise awkward protocols (i.e. that don’t work through NAT) to pass into a NATed site without any problems.

## 27.5 VPN implementation details

Now we'll look in more detail at how a VPN configuration works in a wider context. Figure 27.7 shows the network we've just configured, but box A has a second VPN configured, to connect to network 172.16.16.0, and users at Alice's site also connect to other, non-VPN sites on the Internet – for normal Web surfing, sending e-mail, etc.

![](img/a2132b646d336d5f9a21102d6320e537_729_0.png)

This is where the SPD (security policy database) comes in. When box A receives an outgoing packet from Alice, it inspects the packet contents and compares them against its SPD. If the packet's final destination (and port, etc.) match an entry in the SPD, box A transforms (i.e. encrypts) it and forwards it to the appropriate security gateway. In this respect box A is acting as a router, and the SPD is like a set of routing tables, but with extra VPN functionality added in.

If a packet from Alice doesn't match an entry in the SPD, box A doesn't modify the packet at all and just sends it on its way. In fact, SPDs have a third option (in addition to VPNing, and forwarding without VPNing) and that's to block the packet. This lets the VPN administrator restrict what users at Alice's site can do. For example, if Alice's site is a small branch, you might want its users only to be able to contact HQ (site 192.160.0.0, say) and maybe one other branch (172.16.16.0, say) but *not* be able to access the Internet directly. All external traffic should either be blocked, or more likely routed to HQ where virus-scanning, content-filtering, etc. is performed. Configurations like this let you use the Internet as a cost-effective way to connect remote sites to HQ, but to implement extra security mechanisms centrally – to minimize costs of licenses, server hardware, and system management. This configuration is especially useful for traveling laptops: you want to make sure that users don't collect viruses and all sorts of other rubbish by accessing the Internet in an uncontrolled way. Otherwise, when they subsequently connect to HQ over VPN they might infect your whole network.

### Protocols for VPN

When Alice sends a **ping** request to Bob, the packet looks like:

| src IP | dst IP | proto | payload |
| :--- | :--- | :--- | :--- |
| 10.4.4.41 | 192.168.0.86 | ICMP | ping request |

When the packet has been transformed by VPN, it looks like:

| src IP | dst IP | proto | SPI |
| :--- | :--- | :--- | :--- |
| 192.0.2.42 | 1.2.3.87 | (VPN) | 5001 | *encrypted payload* |

The original packet, including its source and destination addresses and the field identifying it as ICMP protocol, has been encrypted; these encrypted data form the payload of the VPN packet. The new packet is no longer an ICMP packet. (It can’t be, because ICMP doesn’t use SPIs and doesn’t contain encrypted payloads of variable lengths like VPN does.) In fact, VPN uses its own protocol types:

| Protocol | Name | IP proto No. | Description |
| :--- | :--- | :--- | :--- |
| ESP | Encapsulating Security Payload | 50 | encrypted and authenticated |
| AH | Authentication Header | 51 | authenticated only |

Note that these are protocol numbers, not port numbers. You only have port numbers with TCP and UDP, and ESP and AH are separate protocols in their own right. (Recall from Module 15.3 that the IP protocol numbers for UDP and TCP are 6 and 17.) This distinction is important for understanding VPN, and for troubleshooting, as we’ll see in Module 27.9.

You can easily see the protocol numbers (or names) in sniffer traces: below tcpdump shows the original ping packet travelling from Alice to box A:

```
10.4.4.41 > 192.168.0.86: icmp: echo request
```

Figure 27.8 is an *etheral* trace of the encrypted packet sent from box-A to box-B; you can see the SPI (5001) in the packet, but the original ICMP payload and IP address information are encrypted, so *etheral* can’t see what they are.

![](img/a2132b646d336d5f9a21102d6320e537_730_0.png)

In the next module we move on to look at automated keying using IKE.

## 27.6 IKE – Internet Key Exchange (automated keying)

Manual keying is simple to configure. However, it has disadvantages:

- Manually exchanging 32-digit hex keys (over the phone or however you choose to do it) is error-prone and/or insecure
- If you have 100 sites, to manually configure VPNs between each of them you have to set up 100 × 99 VPN tunnels (as each site has a tunnel to each of the other 99 sites). This isn't a very maintainable configuration
- If a hacker breaks your encryption, then they can read your future traffic and any traffic of yours that they've archived from the past, because the key never changes. And, the more you use a given key, the more data you're giving the hacker to analyze, to help them break the key.

*IKE (Internet Key Exchange)* addresses these issues. It provides a secure way to negotiate and exchange keys between sites, automatically, without any human intervention. Once the keys have been exchanged, they are used in security associations (SAs) just like with manual keying. In other words, setting up a VPN has two distinct parts:

- Exchange keys between the two ends of the VPN. This is done either manually or with IKE
- Use the keys to encrypt or authenticate the traffic over the VPN.

As well as making it easier to exchange keys, IKE has other advantages:

- Because keys can now be exchanged automatically, you can automatically change keys ("rekey") frequently, e.g. every few hours
- By regularly changing keys, as long as the keys are generated in a particular way, you can have *perfect forward secrecy* (*PFS*) – breaking a key allows you to read only data encrypted with that key but doesn't makes it any easier to break earlier or later keys. So if a hacker breaks a key, they can read a few hours' worth of your traffic, but to read the next lot of traffic they have to break the new key from scratch. Breaking keys can take months or years, if it's possible at all, so you can see the big improvement in security that IKE can give you over manual keying.

### How IKE works

IKE is divided into two *phases*. For simplicity we'll assume that we're still working with the same two VPN devices, box-A and box-B (Figure 27.7 in the previous Module).

Phase 1: box-A and box-B set up a secure (encrypted) communications channel between them and authenticate themselves to one another. This channel is only used by IKE, not by IPsec itself (i.e. ESP or AH) for transmitting the end-user packets.

Phase 2: over the channel established in Phase 1, IKE on the two boxes negotiates security associations and keys to be used by ESP or AH for sending the end-user packets.

Now both ends have agreed on SAs and keys, and they can encrypt/authenticate the users' packets, using ESP or AH, just as we saw with manual keying.

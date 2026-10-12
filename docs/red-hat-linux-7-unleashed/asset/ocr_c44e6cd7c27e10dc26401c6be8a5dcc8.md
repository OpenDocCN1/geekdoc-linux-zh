networks to listen to, and which ones to mask out. To see this masking in action you would first need to visualize which bits are common between the two ranges. Wherever the bits match, the corresponding bit in the netmask becomes a 1.

> To simplify the exchange of routing information, and to lower the odds of human error in defining a netmask, it is illegal to have discontinuous 1 bits in the netmask. Once you calculate the first 0 bit in the netmask, all of the remain-ing bits must be 0.

```
00001010 10101000 00000000 00000000 (10.168.0.0) Start of Range
00001010 10101000 11111111 11111111 (10.168.255.255) End of Range

11111111 11111111 00000000 00000000 (255.255.0.0) Netmask
```

> Because this example network starts with a 0 (00001010), it would have tradi-tionally been called a class A network. By using the new rules defined by CIDR, it's now effectively in a class B size.

Instead of representing this network by its network number (lowest IP address of an IP network) and its netmask, in CIDR notation you simply count up all of the on bits (1s) in the netmask and represent this network as 10.168.0.0/16. This network is now said to be a 16-bit network. The traditional class C network is another example of a 16-bit network.

# Subnetting

The act of dividing an IP network into smaller subnetworks is called *subnetting*. It is usu-ally done when an organization has a block of addresses that it needs to share between two or more physically separate sites. For example, an organization may request a 24-bit block of addresses for use on the Internet, and then need to share those addresses between two offices. Instead of wasting two full 24-bit networks, you can cut the 24-bit network into two different networks by extending your netmask one more bit. This changes your netmask from 255.255.255.0 (*24* is, a.k.a., */24*) to 255.255.255.128 (*25* is, a.k.a., */25*). This netmask is applied to both of the newly created networks. Where you once had a network of 192.168.1.0/24, you now have two networks of 192.168.1.0/25 and 192.168.1.128/25. The 192.168.1.0/25 network has a host range of 0–127, where
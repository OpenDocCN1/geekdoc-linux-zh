among identical servers 10.10.10.1, 10.10.10.2, and 10.10.10.3. Just modify the commands in the previous example, as shown in Listing 9.7.

# Listing 9.7 Sample iptables LS NAT configuration

```
iptables -t nat -A POSTROUTING -s 10.10.10.1 -o eth0 -j SNAT --to

208.209.210.1
```

```
iptables -t nat -A PREROUTING -s 208.209.210.1 -i eth0 -j DNAT --to

10.10.10.1-10.10.10.3
```

The only difference between Listing 9.7 and Listing 9.6 is that the second rule is translating the incoming 208.209.201.1 destination into the range 10.10.10.1–10.10.10.3, rather than the single 10.10.10.1 address.

# In Sum

Building a Linux firewall is conceptually easy, but the devil is in the details. This chapter has walked you through the general concept of packet filtering and its implementation in the Linux kernel. You’ve learned about two user space tools that you can use to define the necessary filtering rules: ipchains (introduced with kernel 2.1), and the newer iptables (introduced with kernel 2.3). You got a chance to look at a number of detailed network scenarios, and you’ve seen several sample iptables configurations that reflecting several different security policies.

Although the initial cost of deploying a Linux firewall will be lower than many commercial alternatives, crafting a configuration to reflect your security policy takes some serious attention to detail. Packet filtering is your first level of perimeter defense, but a comprehensive security stance will make use of protection at the transport and application layer as well. In the next chapter of this book, we shift our focus to transport-layer firewalls, when you’ll get a close look at the SOCKS proxying protocol.
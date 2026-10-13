# Recommended Changes to Default Rules

It recommends changes to default rules that are appropriate on bastion servers such as the VMs configured early in this book. The default is

```
:INPUT ACCEPT [0:0]
:FORWARD ACCEPT [0:0]
```

The NSA recommendation would change this to

```
:INPUT DROP [0:0]
:FORWARD DROP [0:0]
```

While the rules that allow network traffic into the system still apply, these changes provide another limit on traffic into a system, and traffic that may be forwarded to another system.

Just be careful. When I tried these changes on a gateway system, specifically the physical host system for my VMs, it stopped communication by dropping packets between VMs and external networks. I should have limited such changes to the VMs. So test any changes before implementing them on production systems.

# Regulate the ping Command

One earlier attack on various Internet systems involved the ping command. From Linux, it's possible to flood another system with the -f switch. It may transmit thousands of packets per second. It's important to be able to defend a system from such attacks, as they can prevent others from accessing your web sites and more.

![](bbox=[0.05, 0.7, 0.15, 0.85])

> The -f switch to the ping command was described solely to point out one of the major risks on a network. In many cases, it is illegal to run such a command on or against someone else's system. For example, one Wikipedia article suggests that such an attack could be a violation of the Police and Justice Act in the United Kingdom with a penalty of up to ten years in prison. Similar laws exist in other countries.

One potentially troublesome rule in the default firewall is

```
-A INPUT -p icmp -j ACCEPT
```

However, ICMP messages go both ways. If you run the ping command on a remote system, the remote system responds with an ICMP packet. So if you want to limit ICMP messages, the following rules allow “acceptable” responses to a ping:
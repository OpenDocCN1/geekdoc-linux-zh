defined constant. Then, on system startup, activate defragging by giving the bash shell command

```
```bash
echo 1 > /proc/sys/net/ipv4/ip_always_defrag
```
```

or the tesh shell command

```
```bash
echo 1 >! /proc/sys/net/ipv4/ip_always_defrag
```
```

This will cause the firewall system to reassemble all packets that the sender is intending to transmit. Then, the reassembled packet will be subject to the firewall rules properly. This also has the substantial advantage that corrupted fragments will *not* be passed on to possibly vulnerable systems inside the firewall. Although IP Chains has the capability to block all subsequent fragments, this will both block legitimate traffic and inflict corupt packets on “inside” systems that are vulnerable to these attacks.

# ## B.16 IP Masquerading Fails for ICMP

![](bbox=[0.09, 0.45, 0.97, 0.52])

IP Masquerading (NAT) has several major advantages for security:

+   1. It prevents many attacks against an internal network from the Internet, because it prevents a system on the Internet from addressing internal systems. (A cracker still can attack ports on the firewall that are being mapped to internal systems in the hope of accidentally hitting one with the correct spoofed source address and port, but this is rare so far.)
2. It makes it hard for an attacker to map out someone’s internal network because he “can’t get there from here.”
3. It allows many internal systems to have Internet access without needing multiple real IP addresses.

Conversely, a serious bug in IP Tables does allow the cracker to get there. This bug prevents any ICMP message originating from an internal system from being Masqueraded. Instead, an ICMP error response will have as its payload the source address of the internal system. This allows a cracker to map out your internal network.

This serious problem, along with other design flaws (such as a lack of the simple -l flag for logging that IP Chains has), causes me to consider IP Tables still to be in beta stage and not to be a clear winner over IP Chains. This bug is in all versions of IP Tables before 1.2.6a and affects kernels between 2.4.4 and at least 2.4.19, and affects DNAT when routed to internal systems (and possibly other scenarios).
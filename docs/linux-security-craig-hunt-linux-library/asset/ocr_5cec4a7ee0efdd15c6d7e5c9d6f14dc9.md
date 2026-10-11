+   - The `-i` (interface descriptor) flag now designates the *incoming* interface and only works in the input and forward chains. If you need an interface descriptor for a rule in the forward or output chains, use the `-o` flag instead.

+   - The `iptables` `-y` flag (to match IP packets with the SYN bit set) is now `--syn`.

+   - You can now zero a single chain (with the `-Z` option) while listing it. (This capability did not work in `iptables`.)

+   - Zeroing built-in chains clears policy counters (also a bug fix).

+   - REJECT and LOG chain actions are now extended targets (separate kernel modules).

+   - Chain names can now be up to 31 characters.

+   - The `iptables`'s MASQ chain is now called MASQUERADE and uses a different syntax (see the section “Network Address Translation”).

Figure 9.2 shows the flow of packets as they move around the kernel and shows where the three chains fit within the overall process flow.

# Figure 9.2 Linux kernel packet-filtering built-in chains

![](bbox=[0.15, 0.65, 0.87, 0.82])

As discussed in the “Using iptables” section, a *chain* is the term used to describe a set of rules that are checked in sequence. These rules determine what is done with the packets. Consider the following example:

```
```bash
[ramon]$ sudo iptables -A INPUT -p tcp --dport smtp -j ACCEPT
[ramon]$ sudo iptables -A INPUT -j DROP
```
```

This simple example adds two rules to the input built-in chain. The first rule matches all packets whose transport layer protocol is TCP and whose destination TCP port is 25 (Internet mail or SMTP). If a packet matches this rule, Netfilter is to accept this packet.
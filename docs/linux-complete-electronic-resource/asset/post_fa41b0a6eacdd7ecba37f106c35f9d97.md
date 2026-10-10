
Any other target indicates a user-defined chain (as described in the "Operations on Masquerading" section later in this chapter). The packet will begin traversing the rules in that chain. If that chain doesn't decide the fate of the packet, then once traversal on that chain has finished, traversal resumes on the next rule in the current chain.

Consider two (silly) chains in Figure 14.2: input (the built-in chain) and Test (a user-defined chain).

![](img/a3584dae761d2e3abed8bf40d7637389_559_0.png)

Consider a TCP packet coming from 192.168.1.1, going to 1.2.3.4. It enters the input chain and gets tested against Rule1 - no match. Rule2 matches and its target is Test, so the next rule examined is the start of Test. Rule1 in Test matches but doesn't specify a target, so the next rule is examined, Rule2. This doesn't match, so we have reached the end of the chain. We return to the input chain, where we had just examined Rule2, so we now examine Rule3, which doesn't match either.

The packet path is shown in Figure 14.3.

![](img/a3584dae761d2e3abed8bf40d7637389_559_1.png)

See the "How to Organize Your Firewall Rules" section later in this chapter for ways to use user-defined chains effectively.

## Logging Packets

A side effect of matching a rule is that you can have the matching packet logged using the `-l` flag. You will usually not want this for routine packets, but it is a useful feature if you want to look for exceptional events.

The kernel logs this information and it looks like:

```
Packet log: input DENY eth0 PROTO=17  192.168.2.1:53
    192.168.1.1:1025 L=34 S=0x00 I=18 F=0x0000 T=254
```

This log message is designed to be terse and contain technical information useful only to networking gurus, but it can be useful to the rest of us. It breaks down like so:

- **input**: The chain that contained the rule that matched the packet, causing the log message.
- **DENY**: What the rule said to do to the packet. If this is "*" then the rule didn't effect the packet at all (an accounting rule).
- **eth0**: The interface name. Because this was the input chain, it means that the packet came in on eth0.
- **PROTO=17**: The packet was protocol 17. A list of protocol numbers is given in `/etc/protocols`. The most common are 1 (ICMP), 6 (TCP), and 17 (UDP).
- **192.168.2.1**: The packet’s source IP address was 192.168.2.1.
- **:53**: The source port was port 53. Looking in `/etc/services` shows that this is the domain port (that is, this is probably a DNS reply). For UDP and TCP, this number is the source port. For ICMP, it’s the ICMP type. For others, it will be 65535.
- **192.168.1.1**: The destination IP address.
- **:1025**: The destination port was 1025. For UDP and TCP, this number is the destination port. For ICMP, it’s the ICMP code. For others, it will be 65535.
- **L=34**: The packet was a total of 34 bytes long.
- **S=0x00**: The Type of Service field (divide by 4 to get the Type of Service as used by ipchains).
- **I=18**: The IP ID.
- **F=0x0000**: The 16-bit fragment offset plus flags. A value starting with 0x4 or 0x5 means that the Don’t Fragment bit is set. 0x2 or 0x3 means the More Fragments bit is set; expect more fragments after this. The rest of the number is the offset of this fragment, divided by 8.
- **T=254**: The Time to Live of the packet. One is subtracted from this value for every hop; it usually starts at 15 or 255.

On standard Linux systems, this kernel output is captured by `klogd` (the kernel logging daemon) which hands it to `syslogd` (the system logging daemon). The `/etc/syslog.conf` controls the behavior of `syslogd`, by specifying a destination for each facility (in our case, the facility is `kernel`) and level (for `ipchains`, the level used is `info`).

For example, my (Debian) `/etc/syslog.conf` contains two lines which match `kern.info`:

```
kern.*                              -/var/log/kern.log
*,=info;*,=notice;*,=warn;\
auth,authpriv.none;\
cron,daemon.none;\
mail,news.none            -/var/log/messages
```

These mean that the messages are duplicated in `/var/log/kern.log` and `/var/log/messages`. For more details, see `man syslog.conf`.

## Manipulating the Type of Service

There are four seldom-used bits in the IP header, called the Type of Service (TOS) bits. They affect the way packets are treated; the four bits are Minimum Delay, Maximum Throughput, Maximum Reliability, and Minimum Cost. Only one of these bits is allowed to be set. Rob van Nieuwkerk, the author of the TOS-mangling code, puts it as follows:

> Especially the "Minimum Delay" is important for me. I switch it on for "interactive" packets in my upstream (Linux) router. I'm behind a 336k modem link. Linux prioritizes packets in 3 queues. This way I get acceptable interactive performance while doing full downloads at the same time. (It could even be better if you wasn't such a big queue in the serial driver, but latency is kept down 1.5 seconds now.)

**NOTE**

Obviously, you have no control over incoming packets; you can only control the priority of packets leaving your box. To negotiate priorities with the other end, a protocol like RSVP (which I know nothing about, so don't ask me!) must be used.

The most common use is to set telnet and ftp control connections to Minimum Delay and FTP data to Maximum Throughput. This would be done as follows:

```
ipchains -A output -p tcp -d 0.0.0.0/0 telnet -t 0x01 0x10
ipchains -A output -p tcp -d 0.0.0.0/0 ftp -t 0x01 0x10
ipchains -A output -p tcp -S 0.0.0.0/0 ftp-data \ -t 0x01 0x08
```

The `-t` flag takes two extra parameters, both in hexadecimal. These allow complex twiddling of the TOS bits: The first mask is ANDed with the packet's current TOS, and then the second mask is XORed with it. If this is too confusing, just use the following table:

| **TOS NAME** | **VALUE** | **TYPICAL USES** |
| :--- | :--- | :--- |
| Minimum delay | 0x01 0x10 | ftp, telnet |
| Maximum throughput | 0x01 0x08 | ftp-data |
| Maximum reliability | 0x01 0x04 | Snmp |
| Minimum cost | 0x01 0x02 | nntp |

Andi Kleen goes on to point out the following (mildly edited for posterity):

> Maybe it would be useful to add a reference to the txqueuelen parameter of ifconfig to the discussion of TOS bits. The default device queue length is tuned for ethernet cards, on modems it is too long and makes the 3 band scheduler (which queues based on TOS) work suboptimally. It is a good idea to set it to a value between 4-10 on modem or single b channel ISDN links; on bundled devices an longer queue is needed.
> 
> This is a 2.o and 2.1 problem, but in 2.1 it is an ifconfig flag (with recent nettools), while in 2.0 it requires source patches in the device drivers to change.

So, to see maximal benefits of TOS manipulation for modem PPP links, do `ifconfig $1 txqueuelen` in your `/etc/ppp/ip-up-script`. The number to use depends on the modem speed and the amount of buffering in the modem; here’s Andi to set me straight again:

> The best value for a given configuration needs experiment. If the queues are too short on a router then packets will get dropped. Also, of course one gets benefits even without TOS rewriting, just that TOS rewriting helps to give the benefits to non-cooperating programs (but all standard Linux programs are cooperating).

## Marking a Packet

This allows complex and powerful interactions with Alexey Kuznetsov’s new Quality of Service implementation, as well as the mark-based forwarding in later 2.1 series kernels. More news as it comes to hand. This option is ignored altogether in the 2.0 kernel series.

## Operations on an Entire Chain

A very useful feature of `ipchains` is the ability to group related rules into chains. You can call the chains whatever you want, as long as the names don’t clash with the built-in chains (`input`, `output`, and `forward`) or the targets (`MASQ`, `REDIRECT`, `ACCEPT`, `DENY`, `REJECT`, or `RETURN`). I suggest avoiding upper-case labels entirely, since I may use these for future extensions. The chain name can be up to 8 characters long.

## Creating a New Chain

Let’s create a new chain. Because I am such an imaginative fellow, I’ll call it `test`.

```
# ipchains -N test
#
```

It’s that simple. Now you can put rules in it as detailed previously.

## Deleting a Chain

Deleting a chain is simple as well.

```
# ipchains -X test
#
```

Why -X? Well, all the good letters were taken.

There are a couple of restrictions to deleting chains: they must be empty (see “Flushing a Chain” next) and they must not be the target of any rule. You can’t delete any of the three built-in chains.

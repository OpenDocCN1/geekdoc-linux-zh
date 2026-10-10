
## IP Chains

![](img/a3584dae761d2e3abed8bf40d7637389_550_0.png)

**Figure 14.1:** A packet coming into a machine

**Input chain** This is the first firewall chain against which the packet will be tested. If the verdict of the chain is not **DENY** or **REJECT**, the packet continues on.

**De-masquerade** If the packet is a reply to a previously masqueraded packet, it is de-masqueraded and skips straight to the **output** chain. If you don't use IP Masquerading, you can mentally erase this from the diagram.

**Routing decision** The destination field is examined by the routing code, to decide if this packet should go to a local process (see "local process" defined next) or be forwarded to a remote machine (see the "**forward**" definition).

**Local process** A process running on the machine can receive packets after the Routing Decision step and send packets. (These go through the Routing Decision step, then traverse the **output** chain.)

**Lo interface** This interface is for packets from a local process that are destined for a local process. They will go through the **output** chain with interface set to **lo**, then return through the input chain with interface also lo. The lo interface is usually called the loopback interface.

**Local** If the packet was not created by a local process then the *forward chain* is checked, otherwise the packet goes to the output chain.

**Forward chain** This chain is traversed by any packets that are attempting to pass through this machine to another.

**Output chain** This chain is traversed by all packets just before they are sent out.

## Using ipchains

First, check that you have the version of `ipchains` that this document refers to:

```
$ ipchains --version
ipchains 1.3.8, 27-Oct-1998
```

`ipchains` has a fairly detailed manual page (man `ipchains`), but if you need more detail on particulars, you can check out the programming interface (man 4 `ipfw`) or the file `net/ipv4/ipfw.c` in the 2.1.x kernel source, which is (obviously) authoritative.

There is also an excellent quick reference card by Scott Bronson in the source package, in both A4 and US Letter PostScript™.

There are several different things you can do with `ipchains`. First, there are operations to manage whole chains. You start with three built-in chains, `input`, `output`, and `forward`, which you can't delete. The command line options for whole-chain operations are

- Create a new chain (-N)
- Delete an empty chain (-X)
- Change the policy for a built-in chain. (-P)
- List the rules in a chain (-L)
- Flush the rules out of a chain (-F)
- Zero the packet and byte counters on all rules in a chain (-Z)

There are several ways to manipulate rules inside a chain:

- Append a new rule to a chain (-A)
- Insert a new rule at some position in a chain (-I)
- Replace a rule at some position in a chain (-R)
- Delete a rule at some position in a chain (-D)
- Delete the first rule that matches in a chain (-D)

There are a few operations for masquerading, which are in ipchains for want of a good place to put them:

- List the currently masqueraded connections (-M-L)
- Set masquerading timeout values (-M-S) (But read about a common masquerading timeout problem in the "Common Problems" section later in this chapter.)

The final (and perhaps the most useful) function allows you to check what would happen to a given packet if it were to traverse a given chain.

## Operations on a Single Rule

This is the bread and butter of ipchains—manipulating rules. Most commonly, you will probably use the append (-A) and delete (-D) commands. The others (-I for insert and -R for replace) are simple extensions of these concepts.

Each rule specifies a set of conditions the packet must meet and what to do if it meets them (a target). For example, you might want to deny all ICMP packets coming from the IP address 127.0.0.1. In this case our conditions are that the protocol must be ICMP and the source address must be 127.0.0.1. Our target is DENY.

127.0.0.1 is the loopback interface, which you will have even if you have no real network connection. You can use the ping program to generate such packets (it simply sends an ICMP type 8 [echo request], which all cooperative hosts should obligingly respond to with an ICMP type 0 [echo reply] packet). This makes it useful for testing.

```
# ping -c 1 127.0.0.1
PING 127.0.0.1 (127.0.0.1): 56 data bytes
64 bytes from 127.0.0.1: icmp_seq=0 ttl=64 time=0.2 ms

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 1 packets received, 0% packet loss
round-trip min/avg/max = 0.2/0.2/0.2 ms
# ipchains -A input -s 127.0.0.1 -p icmp -j DENY
# ping -c 1 127.0.0.1
PING 127.0.0.1 (127.0.0.1): 56 data bytes

--- 127.0.0.1 ping statistics ---
1 packets transmitted, 0 packets received, 100% packet loss
#
```

You can see here that the first ping succeeds (the -c 1 tells ping to only send a single packet).

Then we append (-A) to the input chain, a rule specifying that for packets from 127.0.0.1 (-s 127.0.0.1) with protocol ICMP (-p icmp) we should jump to DENY (-j DENY).

Then we test our rule, using the second ping. There will be a pause before the program gives up waiting for a response that will never come.

We can delete the rule in one of two ways. First, since we know that it is the only rule in the input chain, we can use a numbered delete, such as:

```
# ipchains -D input 1
```

This will delete rule number 1 in the input chain.

The second way is to mirror the -A command, but replace the -A with -D. This is useful when you have a complex chain of rules and you don't want to have to count them to figure out that it's rule 37 that you want to get rid of. In this case, we would use:

```
# ipchains -D input -s 127.0.0.1 -p icmp -j DENY
```

The syntax of -D must have exactly the same options as the -A (or -I or -R) command. If there are multiple identical rules in the same chain, only the first one will be deleted.

## Filtering Specifications

We've seen the use of -p to specify protocol and -s to specify source address, but there are other options we can use to specify packet characteristics. What follows is an exhaustive compendium.

**Specifying Source and Destination IP Addresses** Source (-s) and destination (-d) IP addresses can be specified in four ways. The most common way is to use the full name, such as localhost or www.linux.com. The second way is to specify the IP address such as 127.0.0.1.

The third and fourth ways allow specification of a group of IP addresses, such as 199.95.207.0/24 or 199.95.207.0/255.255.255.0. These both specify any IP address from 199.95.207.0 to 199.95.207.255 inclusive; the digits after the "/" tell which parts of the IP address are significant. /32 or /255.255.255.255 is the default (match all of the IP address). To specify any IP address at all, /0 can be used, like so:

```bash
# ipchains -A input -s 0/0 -j DENY
#
```

This is rarely used, as the effect above is the same as not specifying the -s option at all.

**Specifying Inversion** Many flags, including the -s and -d flags can have their arguments preceded by “!” (pronounced “not”) to match addresses not equal to the ones given. For example, -s ! localhost matches any packet not coming from localhost.

**Specifying Protocol** The protocol can be specified with the -p flag. Protocol can be a number (if you know the numeric protocol values for IP) or a name for the special cases of TCP, UDP, or ICMP. Case doesn’t matter, so tcp works as well as TCP.

The protocol name can be prefixed by a ! to invert it, as in -p ! TCP.

**Specifying UDP and TCP Ports** For the special case where a protocol of TCP or UDP is specified, there can be an extra argument indicating the TCP or UDP port or an (inclusive) range of ports (but see the “Handling Fragments” section later in this chapter). A range is represented using a “:” character, such as 6000:6010, which covers 11 port numbers from 6000 to 6010 inclusive. If the lower bound is omitted, it defaults to 0. If the upper bound is omitted, it defaults to 65535. To specify TCP connections coming from ports under 1024, the syntax would be -p TCP -s 0.0.0.0/0 :0.1023. Port numbers can be specified by name, e.g., www.

Note that the port specification can be preceded by a “!”, which inverts it. So to specify every TCP packet BUT a www packet, you would specify -p TCP -d 0.0.0.0/0 ! www.

It is important to realize that the specification -p TCP -d ! 192.168.1.1 www is very different from -p TCP -d 192.168.1.1 ! www.

The first specifies any TCP packet to the www port on any machine but 192.168.1.1. The second specifies any TCP connection to any port on 192.168.1.1 but the www port.

Finally, this case means not the www port and not 192.168.1.1: -p TCP -d ! 192.168.1.1 ! www.

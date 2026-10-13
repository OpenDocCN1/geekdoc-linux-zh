
## ADDING A RULE

A rule can be added using the -A (append), -I (insert), and -R (replace) options. For the ipchains command. A rule specifies a set of conditions a packet must meet. For example, to deny all ping packets coming from the IP address `10.0.0.1`, add the following rule to the input chain:

```bash
# ipchains -A input -s 10.0.0.1 -p icmp -j DENY
```

You can verify that this rule has been added to the input chain by listing rules in the input chain as follows:

```text
# ipchains -n -L input
Chain input (policy ACCEPT):
target     prot opt     source               destination          ports
DENY       icmp - -----  10.0.0.1            0.0.0.0/0             any -> *
```

## DELETING A RULE

A rule can be deleted in one of two ways: by specifying the exact rule number in the chain or by specifying the exact rule. If we know the rule we want to delete is the first rule in the input chain, we can delete it with the following command:

```bash
# ipchains -D input 1
```

Alternately, if we know the rule definition we can delete the rule in the same way we appended a rule while replacing the -A flag with -D. For example, the following command deletes the rules we previously appended to the input chain:

```bash
# ipchains -D input -s 10.0.0.1 -p icmp -j DENY
```

## SPECIFYING SOURCE AND DESTINATION IP ADDRESSES

Source or destination IP addresses can be specified in rules in several ways:

- As simple IP addresses as in the case of `10.10.10.1`.
- As a combination of an IP address and a network mask as in the case of `10.10.10.1/255.255.255.0`.
- As a combination of an IP address and the number of bits which belong to the network portion of the address as in `10.10.10.1/24`.

To specify any and all IP addresses, the address and network mask combination should be specified as `0.0.0.0/0` or `0.0.0.0/0.0.0.0`.

## Specifying Protocols

Protocols are specified with the -p flag as names or numbers. When protocols are specified by name, case does not matter; for instance tcp and UDP indicate the same protocol.

## Specifying UDP and TCP Ports

When UDP or TCP protocols are specified, an extra argument can be passed to specify the UDP or TCP port number, or a range of port numbers. For instance, the following command accepts TCP packets destined for the host 10.10.10.1 on the WWW port (which is port 80):

```bash
# ipchains -A input -p TCP -d 10.10.10.1/24 www -j ACCEPT
```

The following command uses a range of ports to deny access to packets destined for the host 10.10.10.1 between ports 6000 and 6009:

```bash
# ipchains -A input -p TCP -d 10.10.10.1/24 6000:6009 -j DENY
```

Open-ended port ranges can also be defined as in the following command, which defines a rule to deny all packets bound for any host below port 1024:

```bash
# ipchains -A input -p TCP -d 0.0.0.0/0 :1023 -j DENY
```

## Specifying Inversion

Many ipchains flags such as -s, -d, and -p can be preceded with the ! (not) flag, to invert the meaning of the match. For instance, using ! 10.10.10.1 in a rule will mean all other IP addresses except 10.10.10.1.

The following example allows WWW traffic to all destination IP addresses except 10.10.10.1:

```bash
# ipchains -A input -p TCP -d ! 10.10.10.1 www -j ACCEPT
```

Similarly, the following rule allows all incoming traffic except WWW traffic to all destination hosts:

```bash
# ipchains -A input -p TCP -d 0.0.0.0/0 ! www -j ACCEPT
```

## Specifying ICMP Type and Code

Several ICMP packet types are used for different purposes such as the ping command and routing. The ipchains -h icmp command will display a list of all ICMP type names. Table 19.3 lists commonly used ICMP packet types and their respective names and codes.

**Table 19.3  Commonly Used ICMP Packet Types and Codes**

| Number | Name | Required By |
|---:|---|---|
| 0 | echo-reply | ping |
| 3 | destination-unreachable | Any TCP/UDP traffic |
| 5 | redirect | routing |
| 8 | echo-request | ping |
| 11 | time-exceeded | traceroute |

> **Note**
> 
> The `!` (not) flag cannot be used for ICMP names.

> **Tip**
> 
> Do not block ICMP type 3 messages. They are used by TCP and UDP applications. ICMP packets are used to indicate failure for protocols such as TCP and UDP. If you block these packets you will never receive Host unreachable or No route to host errors; connections will just wait for a reply that never comes. While not fatal in most cases, the failure to receive these messages can be irritating and problematic when troubleshooting connectivity problems.
> 
> ICMP packets are also used in MTU discovery. The TCP implementations in Linux use MTU discovery to calculate the largest packet size that can be sent to a destination without fragmenting. Fragmenting slows performance, especially when occasional fragments are lost. MTU discovery works by sending packets with the Don't Fragment bit set, and then sending smaller packets if it gets an ICMP packet indicating Fragmentation Needed but DF Set (`fragmentation-needed`). This is a type of `destination-unreachable` packet, and if it is never received, the local host will not reduce MTU, and performance will be extremely poor or non-existent.

It is common to block all ICMP redirect messages (type 5) because these can be used to manipulate routing. However good IP stacks have safeguards against this type of manipulation, and therefore this is generally not considered a significant risk.

## SPECIFYING AN INTERFACE

The interface to match is specified with the `-i` option. An interface is the physical device on which a packet arrives or through which a packet leaves the firewall system. The input chain controls the interface for incoming packets. The output chain and the forward chain control the interface for outgoing packets.

You can specify an interface that currently does not exist, but is expected to be operational in the future. When the interface comes up, any existing rules will begin applying to that interface. This is very useful for dial-up PPP links where interfaces come into existence and then cease to exist with regularity.

An interface name that ends with a `+` will match all interfaces which begin with that string. For example, the `eth+` option will match all Ethernet interfaces.

The ! (not) flag can precede an interface name, which will match all interfaces other than the specified one.

## SPECIFYING TCP SYN PACKETS

There can be times when you want to permit TCP connections in one direction and not the other. For example, you have an external Web server and you want to allow connections to it, but you do not want to allow connections originating from that server.

This can be achieved by blocking only those packets that are used to request a connection. These packets are called SYN packets; they have the SYN flag set, and the FIN and ACK flags cleared. By disallowing only SYN packets, connection attempts can be stopped.

The -y flag is used for this purpose: It only applies to the TCP protocol. For example, to deny TCP connection attempts from 10.10.10.1 you can use this command:

```bash
# ipchains -A input -p TCP -s 10.10.10.1 -y -j DENY
```

The ! (not) flag can precede the -y option to match all packets excluding the SYN packets.

## FRAGMENTED PACKETS

When a packet is too large to fit in a single frame, it is divided into fragments, and sent as multiple packets. The fragments are re-assembled at the receiving end to reconstruct the whole packet.

Filtering fragments poses a difficulty because only the first fragment contains certain header information such as the source port, destination port, ICMP type, ICMP code, and the TCP SYN flag. The second and further fragments do not have this information. Therefore filtering rules trying to match this kind of information will succeed with the first fragment but will fail to match further fragments. It is generally safe to let later fragments through, because filtering will discard the first fragment, and without it re-assembly of the packet on the target host will fail. However, bugs are known to exist that will crash a system simply by sending it lots of fragments.

If the firewall machine is the only connection to the external network, then the kernel can be compiled with the option IP: always defragment enabled. This option tells the Linux kernel to reassemble all fragments that pass through it. This is a clean solution.

The other option is to disallow all fragmented packets by specifying the -f flag in a rule as in the following example:

```bash
# ipchains -A output -f -d 10.10.10.1 -j DENY
```

This rule will drop any fragments destined for 10.10.10.1.

## THE FILTERING PROCESS

We have looked at all the different ways rules are used to match packets. We now consider what happens when the packet matches a rule:

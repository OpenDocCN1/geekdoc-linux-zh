
handles various network services itself rather than passing them straight through. In this sense, it is a “proxy” for the systems making the request.

A proxy firewall “hides” from the Internet server the fact that your computer even exists. Furthermore, a proxy firewall will commonly handle all incoming connections from the Internet (such as Web traffic, FTP downloads, and e-mail deliveries). Again, this is to minimize the visibility of your internal network to the outside world.

## Configuring an ipchains filtering firewall

Ipchains works by examining packets as they are sent and received on a network interface and deciding which packets should be delivered and which should be stopped. It does this by examining a list (also called a chain) of rules. It stops at the first rule that matches the packet and examines that rule’s target.

If you have configured a firewall during Red Hat Linux installation, some rules have already been set up for you. These rules are probably quite restrictive. After your system is up and running after installation, the first task you should do is check the current status of your firewall. Do that by typing the following as root user:

```
# ipchains -L
Chain input (policy ACCEPT):
target  prot opt source       destination  ports
ACCEPT  all  --  anywhere       anywhere     n/a
ACCEPT  udp  --  a.myisp.net  anywhere     domain - any
ACCEPT  udp  --  b.myisp.net  anywhere     domain - any
DENY    tcp  --  anywhere       anywhere     any - any
DENY    udp  --  anywhere       anywhere     any - any
Chain forward (policy ACCEPT):
Chain output (policy ACCEPT):
```

Preceding is the output I get when I choose the default firewall settings during Red Hat Linux installation (High security). Notice that only input is restricted. In other words, restrictions are on which services outside users can request. The first ACCEPT line results from a rule that allows all requests made from users on the local system (that is, it allows the loopback driver, as indicated by n/a under ports). With that enabled, you can request any service from your local system without the packet being denied.

The next two ACCEPT lines allow the computers I indicate as my DNS servers (`from /etc/resolv.conf`) to request DNS services (`domain`) from my computer. The last two rules (DENY) result in all tcp and udp requests to be denied that don’t match previous rules.

This default firewall configuration is set up in the `/etc/sysconfig/ipchains` file. When the ipchains service starts during system boot time (`/etc/init.d/ipchains`), the service reads the rules from `/etc/sysconfig/ipchains`. Here is what the rules from that file look like to create the preceding configuration:

```
:input ACCEPT
:forward ACCEPT
:output ACCEPT
-A input -s 0/0 -d 0/0 -i lo -j ACCEPT
-A input -s 192.160.0.253 53 -d 0/0 -p udp -j ACCEPT
-A input -s 192.160.0.254 53 -d 0/0 -p udp -j ACCEPT
-A input -s 0/0 -d 0/0 -p tcp -j DENY
-A input -s 0/0 -d 0/0 -p udp -j DENY
```

Because ipchains rules are cleared and reloaded from this file each time you start your system, I recommend the /etc/sysconfig/ipchains file as a good place to set up your firewall rules. With computer-cracker attacks on the rise, the current approach to security the experts recommend is to be secure by default. This means you should start by restricting most services and should then add only those services you want enabled. Put in the rules that allow services first, and then have all other services denied in the last two lines.

### Understanding ipchains firewall rules

An ipchains target can be a simple command like `ACCEPT` or `DENY`, or it can be the name of another rule chain to begin examining. There are three default rule chains that the kernel will always examine. They are the input, output, and forward chains. You can create additional user-defined chains and call them from these original three, but for simple firewall configurations, the standard three should be sufficient.

> **TIP:** ipchains stops examining a rule chain after finding a match, so pay attention to the order of rules. Rules with specific conditions should go before those with similar but broader conditions. If you accept all TCP connections but follow that with a rule to deny telnet access, telnet (being a TCP service) will be allowed. Reverse the order of the rules (deny telnet, then accept TCP) to have the right effect.

The general syntax is to invoke `ipchains` with a parameter specifying the action to take, followed by the rule chain to take it on. This may be followed by a rule description and a rule target. Table 14-4 shows action parameters you can use with `ipchains`.

#### Table 14-4: Ipchains Action Parameters

| Action Parameter | Description |
| :--- | :--- |
| -A, --append | Append a new rule to the end of the specified list. |
| -D, --delete | Delete a rule from the specified list. You can specify the rule by its numeric place in the list or by the rule parameters that match it. |
| -R, --replace | Replace a rule with a new one. |
| -I, --insert | Insert a new rule into a specific position in the list. |
| -L, --list | List all the rules in a chain. If the chain name is left off, list all rules in all chains. |
| -F, --flush | Flush all the rules out of a chain. |
| -Z, --zero | Zero out the packet counters for all chains. |
| -N, --new-chain | Create a new chain with the specified name. |
| -X, --delete-chain | Delete the chain with the specified name. |
| -P, --policy | Set the policy for the chain to the specified target. The policy of a chain describes what action to take if no rule matches the packet. The default policy for all chains is ACCEPT. |
| -M, --masquerading | Allows viewing of masqueraded connections. IP Masquerading is discussed in Chapter 16. |
| -S, --set | Set the timeouts for TCP, TCPFIN, and UDP packets. |
| -C, --check | Check a supplied packet against the given chain. This is useful mainly for debugging. |
| -h | Print a Help message describing parameters to ipchains. |

As you can see in Table 14-4, the ipchains action parameters can be expressed in two forms, either as a dash followed by a single capital letter, or two dashes followed by a descriptive word. Both will work, so use whichever you prefer. In the example in this chapter, I will use the abbreviated version.

Usually, we follow the action parameter with the rule chain to apply it to. Rules added to the input chain will be examined only when filtering network packets being received by the Linux box. Similarly, the output chain is examined only for packets being transmitted from the Linux box. The forward chain is examined only for network packets that are received by the Linux system but will be delivered to some other network system. Packet forwarding only occurs when your system is configured as a router.

After specifying a chain to act on, you may specify some optional parameters to define a rule. Table 14-5 lists the available optional parameters.

#### Table 14-5: Ipchains Optional Parameters

| Parameter | Description |
| :--- | :--- |
| -p, --protocol [!] protocol | Specify the protocol that the rule should match against. This should be TCP, UDP, or ICMP. |
| -s, --source [!] address | Specify the source address to match against. This can be an individual address, or you can specify an entire subnet by following the address with a / and the number of 1 bits in the left side of the subnet mask. Thus, the address 199.170.177.0/24 would have a subnet mask of 255.255.255.0. |
| --source-port [!] port | The source TCP or UDP port number as specified in /etc/services. You can also specify a range of ports by listing the first and last port number separated by a `:` colon character. |
| -d, --destination [!] address | Specify the destination address to match against. This can be an individual address, or you can specify an entire subnet by following the address with a / and the number of 1 bits in the left side of the subnet mask. Thus, the address 199.170.177.0/24 would have a subnet mask of 255.255.255.0. |
| --destination-port [!] port | The destination TCP or UDP port number as specified in /etc/services. You can also specify a range of ports by listing the first and last port number separated by a `:` colon character. |
| --icmp-type [!] typename | Set the type of ICMP packet to use. |
| -j, --jump target | The name of the target (action) to execute when the rule matches. This could be the name of another ipchain or one of several predefined targets. |
| -i, --interface [!] name | The name of the network interface that this rule applies to. If this option is not supplied, the rule will apply to all interfaces. |
| [!] -f, --fragment | The rule will apply only to fragmented packets, excluding the first packet. In other words, it applies to all packet fragments after the first one. |
| -b, --bidirectional | The rule should apply to both incoming and outgoing packets. |
| -v, --verbose | Print debug messages when processing this ipchains command. |
| -n, --numeric | Use IP addresses instead of host names when printing output to the screen. |

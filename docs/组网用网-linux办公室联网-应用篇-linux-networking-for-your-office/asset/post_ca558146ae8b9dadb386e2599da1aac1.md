
+   - IP: optimize as router not host—If this system will be used primarily as a packet filtering router, and not itself as a server or client, you may want to select Y to this option to slightly improve performance.

You’ll also need additional options for your specific type of network and hardware. For instance, you’ll need all the usual TCP/IP options and drivers for your network card. See Chapter 6, “Compiling a Kernel for Networking,” for more information.

> NOTE
> I’m assuming that you’re using a 2.2.x-series kernel. If you’re using an older or newer kernel, the options you need may be somewhat different from what I describe here.

## Using ipchains

Linux uses sets of rules, known as chains, to determine the fate of packets coming into the computer. When a packet enters a chain, the rules in the chain determine what happens to the packet. Linux applies each rule to each packet in turn, and each rule can cause certain types of packets to be discarded, modified, or accepted.

## Types of Chains

By default, there are three chains on a Linux computer:

- The input chain—This chain processes packets that come into the computer. If you configure an input chain to reject packets from a specific address, your computer will be “blind” to that address, which means that your computer can’t be attacked from that address, at least not directly and if the remote site is honest about its address. If an incoming packet is destined for the local computer, it passes through this chain through the local TCP/IP stack.
- The forward chain—If a packet is destined for a computer on one network, but originates on another, it can be routed (or forwarded) through the current computer. The forwarding chain processes such requests. It is here that IP masquerading occurs. You can also implement many firewall rules in the forwarding chain, although the input and output chains can also be used for this purpose.
- The output chain—When a packet leaves the computer, it must traverse the output chain. Like the input chain, the output chain can accept or deny packets. You could implement rules on an output chain to deny access to certain types of services on external computers. For instance, you could block requests to specific Web sites.

You can also create user-defined chains for special purposes. By default, the three standard chains are empty, meaning that they either deny or accept all packets sent through them, depending upon the default configuration (which is normally to accept all packets). Adding rules to the chain can change acceptance to denial or denial to acceptance for particular packet types.

You manipulate the chains' rules with the ipchains utility. Chapter 20 (p. 476) presents the most important options for manipulating chains. The ipchains manpage contains more details.

## A Simple Example

Here's an example of a script to set up a simple proxy filter firewall. This example script is included on the CD accompanying this book as sams-extras/firewall/firewall.

```
#!/bin/sh
# Setup Internal LAN variables here

IntIF="eth0"      # internal network interface
IntHostIP="192.168.1.1"   # internal host IP
IntNETIP="192.168.1.0/24" # internal LAN IP

# Setup External Internet variables here

ExtIF="eth1"      # external network interface
ExtHostIP="10.0.0.1"   # external host IP
ExtNETIP="10.0.0.0/8"  # external Network IP

IPCHAINS="/sbin/ipchains"

echo -n "*** Flushing all firewall rules and starting clean..."
$IPCHAINS -F input
$IPCHAINS -F output
$IPCHAINS -F forward
echo "done!"

echo -n "*** Setting the default policy to ACCEPT for input, output, and forward..."
$IPCHAINS -P input ACCEPT
$IPCHAINS -P output ACCEPT
$IPCHAINS -P forward ACCEPT
echo "done!"

echo -n "*** Setting up protection against IP spoofing..."
$IPCHAINS -A input -i $ExtIF -d ! $ExtHostIP -j DENY
$IPCHAINS -A input -i $ExtIF -s $IntNETIP -j DENY
$IPCHAINS -A input -i $IntIF -s ! $IntNETIP -j DENY
echo "done!"
```

```
echo -n "*** Reject connections to ad.doubleclick.net..."
$IPCHAINS -A output -p tcp -d 209.67.38.0/24 80 -j REJECT
$IPCHAINS -A output -p tcp -d 199.95.208.0/24 80 -j REJECT
echo "done!"
```

```
echo -n "*** Deny incoming telnet connections..."
$IPCHAINS -A input -i $ExtIF -p tcp -s 0/0 -d $ExtHostIP 23 -j DENY
```

```
echo -n "*** allow local connections only, for X Font Server on port 7100..."
$IPCHAINS -A input -i $ExtIF -p tcp -s $ExtHostIP -d $ExtHostIP 7100 -j ACCEPT
$IPCHAINS -A input -i $ExtIF -p udp -s $ExtHostIP -d $ExtHostIP 7100 -j ACCEPT
$IPCHAINS -A input -i $ExtIF -p tcp -s 0/0 -d $ExtHostIP 7100 -j DENY
$IPCHAINS -A input -i $ExtIF -p udp -s 0/0 -d $ExtHostIP 7100 -j DENY
```

## CAUTION

Be sure the permissions on any script that sets firewall options are set appropriately. Specifically, only root should have write access to the script. It's probably best if only root can read or execute the script, too—in other words, set it for 0700 permissions. The CD mastering process sets the permissions more liberally than this, so if you use the firewall script on the CD as a base, be sure to change the permissions.

Here's a brief rundown of what each section accomplishes:

- Variables—The first few lines of the script set variables used internally. These include the IP addresses of both Ethernet interfaces, the Ethernet interface names, and the location of the ipchains utility.

> NOTE
> The IP addresses used in this script are private network addresses. In reality, the external network address is likely to be a public Internet address, and the internal address will likely be private only if you also enable IP masquerading (which can be done in the same script that configures the rest of the firewall).

- Flushing—The script flushes any existing rules and sets the default policies to ACCEPT, which makes this a fairly lax firewall script.

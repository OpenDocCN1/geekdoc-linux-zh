You can also create user-defined chains for special purposes. By default, the three standard chains are empty, meaning that they either deny or accept all packets sent through them, depending upon the default configuration (which is normally to accept all packets). Adding rules to the chain can change acceptance to denial or denial to acceptance for particular packet types.

You manipulate the chains' rules with the ipchains utility. Chapter 20 (p. 476) presents the most important options for manipulating chains. The ipchains manpage contains more details.

# A Simple Example

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
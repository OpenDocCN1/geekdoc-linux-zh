SSH session. If indeed I have locked myself out, I merely wait a few minutes for the firewall script to run and shut the firewall down, giving me the opportunity to fix the script and try again.

Furthermore, remember that firewall filters are applied in the order in which you've defined them on the INPUT or OUTPUT chain. The rules are appended to the end of their chain in the order in which you define them. The first matching rule wins. Because of this, firewall rules must be defined in a hierarchical order from most specific to more general rules.

Firewall initialization is used to cover a lot of ground, including defining global constants used in the shell script, enabling kernel support features (when necessary), clearing out any existing rules in the firewall chains, defining default policies for the INPUT and OUTPUT chains, re-enabling the loopback interface for normal system operation, denying access from any specific hosts or networks you've decided to block, and defining some basic rules to protect against bad addresses and to protect certain services running on unprivileged ports.

# ## Symbolic Constants Used in the Firewall Examples

A firewall shell script is easiest to read and maintain if symbolic constants are used for recurring names and addresses. The following constants either are used throughout the examples in this chapter or are universal constants defined in the networking standards. This example also includes the “shebang” interpreter line from above as a friendly reminder:

```
#!/bin/sh

IPT="/sbin/iptables"                  # Location of iptables on your system
INTERNET="eth0"                     # Internet-connected interface
LOOPBACK_INTERFACE="lo"             # However your system names it
IPADDR="my_ip.address"             # your IP address
MY_ISP="my_isp.address.range"      # ISP server & NOC address range
SUBNET_BASE="my.subnet.network"    # your subnet's network address
SUBNET_BROADCAST="my.subnet.bcast" # Your subnet's broadcast address
LOOPBACK="127.0.0.0/8"             # reserved loopback address range
CLASS_A="10.0.0.0/8"               # class A private networks
CLASS_B="172.16.0.0/12"            # class B private networks
CLASS_C="192.168.0.0/16"           # class C private networks
CLASS_D_MULTIICAST="224.0.0.0/4"   # class D multicast addresses
CLASS_E_RESERVED_NET="240.0.0.0/5" # class E reserved addresses
BROADCAST_SRC="0.0.0.0"            # broadcast source address
BROADCAST_DEST="255.255.255.255"  # broadcast destination address
PRIVPORTS="10:1023"                # well-known, privileged port range
UNPRIVPORTS="1024:65535"           # unprivileged port range
```

Constants not listed here are defined in the context of the specific rules they are used with.
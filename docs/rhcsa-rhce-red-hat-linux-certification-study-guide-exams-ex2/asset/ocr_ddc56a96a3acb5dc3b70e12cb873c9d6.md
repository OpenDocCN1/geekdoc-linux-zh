```
-A INPUT -p icmp --icmp-type echo-reply -j ACCEPT
-A INPUT -p icmp --icmp-type destination-unreachable -j ACCEPT
-A INPUT -p icmp --icmp-type time-exceeded -j ACCEPT
```

The following rule limits the rate at which a ping command can be applied to a system:

```
-A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT
```

While the Firewall Configuration tool discussed later in this chapter can limit the effect of ICMP messages in most of the same ways, it does not have the ability to regulate the rate of ping network packets accepted onto a system.

# Block Suspicious IP Addresses

Crackers who want to break into a system may hide their source IP address. As nobody is supposed to use a private, multicast, or experimental IPv4 address on the public Internet, such addresses are one way to hide. The following additions to the /etc/sysconfig/iptables file would drop packets sourced from the specified IPv4 network address blocks:

```
-A INPUT -i eth0 -s 10.0.0.0/8 -j DROP
-A INPUT -i eth0 -s 172.16.0.0/12 -j DROP
-A INPUT -i eth0 -s 192.168.0.0/16 -j DROP
-A INPUT -i eth0 -s 224.0.0.0/4 -j DROP
-A INPUT -i eth0 -s 240.0.0.0/5 -j DROP
```

# Regulate Access to SSH

Since SSH is such an important means for the administration of remote systems, additional measures to protect such services are important. It's certainly possible to set up a nonstandard port for SSH communication. Such a measure can be a part of a layered security strategy. However, tools like nmap can detect the use of SSH on such nonstandard ports. So it's generally better to set up the configuration of the SSH server as discussed in Chapter 11 along with firewall rules such as the following. The first rule shown here creates a new chain, SSH_CHAIN, for all TCP traffic to port 22:

```
-A INPUT -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -j SSH_CHAIN
```

The next rule starts the SSH_CHAIN, by limiting access requests to three per minute.

```
-A SSH_CHAIN -i eth0 -p tcp -m tcp --dport 22 -m state --state NEW -m recent
--update --seconds 60 --hitcount 3 --rttl --name SSH -j DROP
```
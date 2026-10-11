```
# Accept incomling ICMP packet of 'echo reply (=0)' type (ping replies)
iptables -A FORWARD -p icmp -i eth0 -d 208.209.210.0/24 \
    --icmp-type 0 -j ACCEPT

# Accept all outgoing ICMP connections entering the private
# interface (eth1)
iptables -A FORWARD -p icmp -i eth1 -j ACCEPT

# Drop all other traffic in the FORWARD chain
iptables -A FORWARD -j DROP
```

Note that the last line is not really needed because you have established a deny policy (where everything is denied by default unless specifically allowed) for the forward chain at the top of the script. However, it’s always a good idea to err on the side of caution.
Next, let’s restrict the previous policy by only allowing SSH, WWW, SMTP, and DNS outbound services (see Listing 9.3).The lines in **boldface** are the changes from the previous scenario in Listing 9.2.

# Listing 9.3  Dual-homed firewall architecture: SSH incoming services, SSH, WWW, SMTP, and DNS outgoing services only

```
# Flush all the rules out of the chains
iptables -F INPUT
iptables -F OUTPUT
iptables -F FORWARD

# Set the default policy for the FORWARD chain to deny all
iptables -P FORWARD deny

# Block all incoming traffic coming from public interface (eth0)
iptables -A INPUT -i eth0 -j DROP

# Block all outgoing traffic going out the public interface (eth0)
iptables -A OUTPUT -o eth0 -j DROP

# Instruct Netfilter to accept fragmented packets (-f)
iptables -A FORWARD -f -j ACCEPT

# Accept incoming TCP packets from established connections
# (--state ESTABLISHED,RELATED)iptables -A FORWARD -m state --state{ESTABLISHED,RELATED} -j ACCEPT
```
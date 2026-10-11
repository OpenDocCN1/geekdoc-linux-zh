# Example 16-41 Firewall Start-up Script (Continued)

```
#
# DHCP addresses are "leased" for a period of time after which
# the address may change, so make sure that this script is
# re-run each time the IP address changes.  See DHCP documentation
#
# Now set the external broadcast address.
# This script only uses the broadcast for DHCP.
#EXXCAST="202.7.1.31"
#
# To get the broadcast address for DHCP uncomment the next line
# EXXCAST=`ifconfig|egrep -A 2 \$EXTIF|awk '/inet/ { print $4 }'\
#   |sed -e s/Bcast\///`
# Now set your internal IP address
INIP="10.1.1.1"       # tocat-ip
# Now set the network variables
INNET="10.0.0.0/8"
# DMZNET="202.7.1.24/30"      # Uncomment this if used
#End of variable section
# Let's be paranoid and enter blocking rules to start
# We'll disable them at the end.  Also we'll allow lo here and
# set up the REJECT policy.
iptchains -F
iptchains -I input 1 -j REJECT
iptchains -I output 1 -j REJECT
iptchains -I forward 1 -j REJECT
iptchains -A input -i lo -s 0/0 -d 0/0 -j ACCEPT
iptchains -A output -i lo -s 0/0 -d 0/0 -j ACCEPT
iptchains -P input REJECT
iptchains -P output REJECT
iptchains -P forward REJECT
#
# initial masquerading requirements
depmod -a
modprobe ip_masq_ftp
echo "1" > /proc/sys/net/ipv4/ip_forward
iptchains -M -S 3600 10 50
# end initial masquerading requirements
# DHCP support requires this...uncomment if necessary
echo "1" > /proc/sys/net/ipv4/ip_dynaddr
# anti-spoofing
for file in /proc/sys/net/ipv4/conf/*/rp_filter
  do
    echo "1" > $file
done
iptchains -A input -i 1 lo -s 127.0.0.0/8 -j REJECT -1
# end anti-spoof
# Internet input rejects
iptchains -A input -i $EXXIF -p tcp -d $INNET -j REJECT -1
iptchains -A input -i $EXXIF -p tcp -d $EXPIP -j REJECT
# end input rejects
# ICMP Custom Chain-catch important ICMP messages
# our catch-all reject rule will drop the rest.
# First create the chain...no problem if it already exists.
# Real problems if it doesn't.
iptchains -N outputN 2>/dev/null
# Now add the rules
iptchains -A icmperr -p icmp --icmp-type destination-unreachable -j ACCEPT
iptchains -A icmperr -p icmp --icmp-type parameter-problem -j ACCEPT
iptchains -A icmperr -p icmp --icmp-type source-quench -j ACCEPT
```
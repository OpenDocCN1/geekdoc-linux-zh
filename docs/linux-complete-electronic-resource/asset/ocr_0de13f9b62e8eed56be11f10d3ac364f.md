before any network interfaces are initialized (for example, Debian users
would put them in /etc/init.d/netbase if they are not already there):

```
# This is the best method: turn on Source Address
# Verification and get spoof protection on all current
# and future interfaces.
if [ -e /proc/sys/net/ipv4/conf/all/rp_filter ]; then
    echo -n "Setting up IP spoofing protection..."
    for f in /proc/sys/net/ipv4/conf/*/rp_filter; do
        echo 1 > $f
    done
    echo "done."
else
    echo PROBLEMS SETTING UP SPOOFING PROTECTION. BE WORRIED.
    echo "CONTROL-D will exit this shell and continue startup."
    echo
    # Start a single user shell on the console
    /sbin/sulogin $CONSOLE
fi
```

If you cannot do this, you can manually insert rules to protect every
interface. This requires knowledge of each interface. The 2.1 kernels auto-
atically reject packets claiming to come from the 127. \*.* addresses
(reserved for the local loopback interface, lo).

For example, say we have three interfaces, eth0, eth1, and ppp0. We
can use ifconfig to tell us the address and netmask of the interfaces.
Say eth0 was attached to a network 192.168.1.0 with netmask
255.255.255.0, eth1 was attached to a network 10.0.0.0 with netmask
255.255.0.0, and ppp0 connected to the Internet (where any address except
the reserved private IP addresses are allowed), we would insert the fol-
lowing rules:

```
# ipchains -A input -i eth0 -s ! 192.168.1.0/255.255.255.0 \
# -j DENY
# ipchains -A input -i ! eth0 -s 192.168.1.0/255.255.255.0 \
# -j DENY
# ipchains -A input -i eth1 -s ! 10.0.0.0/255.0.0.0 -j DENY
# ipchains -A input -i ! eth1 -s 10.0.0.0/255.0.0.0 -j DENY
```

This approach is not as good as the Source Address Verification
approach, because if your network changes you have to change your fire-
walling rules to keep up.

If you are running a 2.0 series kernel, you might want to protect the
loopback interface as well, using a rule like this:

```
# ipchains -A input -i ! lo -s 127.0.0.0/255.0.0.0 -j DENY
```
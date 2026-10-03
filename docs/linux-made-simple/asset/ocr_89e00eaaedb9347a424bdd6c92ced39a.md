```
$ sudo service dnsmasq start
```

Now set all the other internal network machines to use DHCP on the local network and you should discover two things: That the internal network machines can all ping each other (by IP address, once you’ve figured out who’s who) and, further, that while they can’t ping the outside world, they can at least perform name resolution. Dnsmasq will cache queries too, which saves a few milliseconds, should you query the same address more than once. When the client machines obtain a DHCP lease, dnsmasq will push the required gateway and DNS settings automatically, and the clients’ /etc/resolv.conf files will be updated accordingly.

# Packet forwarding

In order to get traffic flowing we need to set up packet forwarding and NAT (Network Address Translation). The first thing to do is to enable packet forwarding in the kernel. You can do this through the /proc interface like so:

```
$ echo 1 > /proc/sys/net/ipv4/ip_forward
```

To make this persist across reboots depends on your distro – some still use the /etc/sysctl.conf file, so add:

```
net.ipv4.ip_forward=1
```

Some (Arch and derivatives) have deprecated this file in favour of individual files in /etc/sysctl.d/. If this is you create a file, say /etc/sysctl.d/40-ip-forward.conf, and add the above line to it. That tells the kernel that forwarding is allowed, but we still have to stipulate the whences and whereto s. We’ll use some good old fashioned iptables rules to do this. It’s certainly possible with the newer nftables framework, but with every distro running a different version, and it still being quite new code, we won’t do that. Since we’re assuming our gateway machine is behind another gateway (that connects to your ISP), we needn’t worry too much about security. So we can tell iptables to forward packets from the outside to our internal network:

```
$ sudo iptables -A FORWARD -i int0 -o ext0 -j ACCEPT
```

If you haven’t previously added any iptables rules of your own then its very likely you won’t need the previous line –

![](bbox=[0.13, 0.61, 0.56, 0.86])

This is what a successful WPA2 handshake should look like, but our hotspot fails to make it warm in here [see Hotspots With Hostapd, p129].

most distros will, by default, allow all packets to be forwarded, as well as allowing everything else. We will need to set up NAT, so that traffic coming out of ext0 can find its way back to int0. This step changes the packets’ source addresses to our gateway’s IP, and keeps track of the connection so that, as if by magic, any responses are forwarded to the correct machine on our internal network.

```
$ sudo iptables -t nat -A POSTROUTING -o ext0 -j MASQUERADE
```

A more robust approach here is to use SNAT (Source NAT) instead of MASQUERADE. This is conditional on the ext0 interface on your gateway having a static IP, though. Note that this has nothing to do with how your ISP assigns IP addresses, merely how you set up your gateway machine’s ext0 interface. Using the following line instead means that NAT-ed connections can better survive link loss:

```
$ sudo iptables -t nat -A POSTROUTING -o ext0 -j SNAT --to-source 192.168.1.127
```

If ext0 does not have the IP address above, then this won’t work, funnily enough. The reason this doesn’t work with a variable address is that if the link is interrupted then it’s possible that upon reconnecting ext0 is assigned a different address. The MASQUERADE target just forgets everything in the event of link loss, so connections can be safely (but slowly) re-established via the new address.

If you’re running services on your internal network, and you want these to be accessible from the external network, then you must set up port forwarding, eg if you have an SSH server running on the machine 10.0.1.1, in order for externally networked machines to see it, they’ll need to connect via the gateway machine 192.168.1.254. Since you might have an SSH server running on the gateway already, we’ll forward its TCP port 2222 to port 22 on the internal machine:

```
$ sudo iptables -t nat -A PREROUTING -i ext0 -p tcp --dport 2222 -j DNAT --to 10.0.1.1:22
```

Now you can connect from the external network by pointing your SSH client at your gateway’s port 2222. If you wanted to connect from the outside world, then you could add another rule which forwards traffic from your primary router to our gateway machine’s port 2222. Once you’ve got everything working it’s good to save your iptables rules. Each distro does this slightly differently, but ultimately rules are saved to a text file with:

```
$ sudo iptables-save > /etc/iptables.rules
```

Some distributions will auto-magically restore firewall rules from this file, others require to be told. Species of the Debian lineage, for example, would require the following line to be added to /etc/network/interfaces:

```
pre-up iptables-restore </etc/iptables.rules
```

# Cutting cords

Sometimes it’s desirable to make your router accessible wirelessly, so that your mobile devices can connect to it. This is particularly useful if you find yourself using said devices in areas of your house with poor wireless coverage: Your gateway machine may be connected to your ISP-supplied box via Powerline Ethernet, and situated in or around the blackspot, bringing light to the darkness. It is also possible for this to work if there is a wireless link instead of a Powerline one, so that we have a simple wireless repeater. This may require two wireless cards in the gateway machine though, since some cards cannot be access points and clients
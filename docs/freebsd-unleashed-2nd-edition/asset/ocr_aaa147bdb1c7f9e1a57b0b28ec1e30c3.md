![](bbox=[0.32, 0.09, 0.64, 0.35])

FIGURE 30.7 Enabling the new security policy using the toggle switch in the nmc program.

# FreeBSD as a VPN Server

It won’t always be the case that you only have one FreeBSD machine to connect to a remote Virtual Private Network. You might have to set up a routed, translated subnetwork of your own, for example, and create a permanent VPN tunnel to the remote network for the use of multiple machines on your own subnet. Fortunately, because you have set up the gif0 interface to use a virtual private IP address on your own local machine, making the jump to a fully routed VPN link should be child’s play.

All that’s required is a second Ethernet card on your machine that’s plugged into the local private network. Follow the same instructions listed in the previous section, except for the part where you alias the private address (192.168.0.1) to the public Ethernet card. Instead, assign that address to the second Ethernet card. Then, set up the spadd lines to reflect the network address of the whole network you’re managing instead of just your own single machine. For instance, the following lines in /etc/ipsec.conf would allow you to tunnel the entire private 192.168.0.0 network (Class B) to the remote VPN server, enabling the machines on your network to communicate with the machines in the remote 10.0.0.0 network, and vice versa:

```
spadd 192.168.0.0/16 10.0.0.0/8 any -P out ipsec
esp/tunnel/111.112.113.114-221.222.223.224/require;
spadd 10.0.0.0/8 192.168.0.0/16 any -P in ipsec
esp/tunnel/221.222.223.224-111.112.113.114/require;
```

# Routing and Firewalling

One final point to note is that to run a proper subnetwork, your FreeBSD machine will have to be doing all the routing and NAT/firewall work for that network; otherwise, you
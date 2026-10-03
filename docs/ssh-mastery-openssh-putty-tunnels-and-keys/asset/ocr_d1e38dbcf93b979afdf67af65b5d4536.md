the operating system via the local tunnel interface.

Just like any other interface you want to use for IP routing, your tunnel interfaces need IP addresses. You must route traffic destined for the remote network to the IP address at the remote end of the tunnel. We’ll demonstrate this in each example.

Each tunnel interface needs a device number, like any other device on a Unix-like system. Just as your network interface might be eth0 or em1, tunnel devices might tun0 or tun1. Our examples use device zero, creating device names like tun0. If you have many tunnel devices I recommend both assigning a specific device for each purpose and reassessing your design choices.

# SSH Server Configuration

The sshd_config keyword PermitTunnel specifies if a client may establish a VPN tunnel. PermitTunnel has four valid options: yes, no, point-to-point, or ethernet. If set to no (the default), tunnels are forbidden. If set to yes, all tunnels are permitted.

A point-to-point tunnel is a virtual private circuit that runs from one spot to another. A point-to-point tunnel requires routing to be usable. This is usually the best type of tunnel for an SSH VPN.

```
PermitTunnel point-to-point
```

An Ethernet tunnel transmits layer 2 traffic, permitting two separate locations to share their local LAN. Don’t tunnel Ethernet over SSH if you can possibly avoid it. Local network problems on one side of the VPN can propagate across the link and saturate your external bandwidth. SSH VPNs are already vulnerable to congestion; don’t amplify that problem even more.

To use an SSH VPN, the SSH processes must have sufficient privileges to make changes to the tunnel devices and the routing table on both the client and the server. Creating an SSH VPN requires root privileges on both the client and the server. You’ll run ssh as root and log in directly as root. I stated earlier that logging in as root is a terrible option. I stand by that statement. If you’re using an SSH VPN, however, you’re basically out of good options.

Here I permit our SSH client a root login on the SSH server, but only through public-key authentication. I also allow that IP address to open a tunnel.

```
Match Address avarice.mwl.io
PermitRootLogin prohibit-password
PermitTunnel point-to-point
```

In your production configuration, use the client’s IP address rather than the hostname.

Very old versions of OpenSSH might not let you put the PermitTunnel statement inside a Match statement. If you encounter such an sshd, immediately upgrade the server’s OpenSSH—it’s not safe to have on the public Internet.
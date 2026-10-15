# 6 VPN WITH SSH

As of version 4.3, OpenSSH can use the tun/tap device to encrypt a tunnel. This is very similar to other TLS based VPN solutions like OpenVPN. One advantage with SSH is that there is no need to install and configure additional software. Additionally the tunnel uses the SSH authentication like pre shared keys. The drawback is that the encapsulation is done over TCP which might result in poor performance on a slow link. Also the tunnel is relying on a single (fragile) TCP connection. This technique is very useful for a quick IP based VPN setup. There is no limitation as with the single TCP port forward, all layer 3/4 protocols like ICMP, TCP/UDP, etc. are forwarded over the VPN. In any case, the following options are needed in the sshd_conf file:

```
PermitRootLogin yes
PermitTunnel yes
```

# 6.1 Single P2P connection

Here we are connecting two hosts, hclient and hserver with a peer to peer tunnel. The connection is started from hclient to hserver and is done as root. The tunnel end points are 10.0.1.1 (server) and 10.0.1.2 (client) and we create a device tun5 (this could also be an other number). The procedure is very simple:

+   - Connect with SSH using the tunnel option -w
+   - Configure the IP addresses of the tunnel. Once on the server and once on the client.

# Connect to the server

Connection started on the client and commands are executed on the server.

# Server is on Linux

```
cli># ssh -w5:5 root@hserver
srv># ifconfig tun5 10.0.1.1 netmask 255.255.255.252    # Executed on the server shell
```

# Server is on FreeBSD

```
cli># ssh -w5:5 root@hserver
srv># ifconfig tun5 10.0.1.1 10.0.1.2                # Executed on the server shell
```

# Configure the client

Commands executed on the client:

```
cli># ifconfig tun5 10.0.1.2 netmask 255.255.255.252    # Client is on Linux
cli># ifconfig tun5 10.0.1.2 10.0.1.1                  # Client is on FreeBSD
```

The two hosts are now connected and can transparently communicate with any layer 3/4 protocol using the tunnel IP addresses.

# 6.2 Connect two networks

In addition to the p2p setup above, it is more useful to connect two private networks with an SSH VPN using two gates. Suppose for the example, netA is 192.168.51.0/24 and netB 192.168.16.0/24. The procedure is similar as above, we only need to add the routing. NAT must be activated on the private interface only if the gates are not the same as the default gateway of their network. 192.168.51.0/24 (netA)|gateA <-> gateB|192.168.16.0/24 (netB)

+   - Connect with SSH using the tunnel option -w.
+   - Configure the IP addresses of the tunnel. Once on the server and once on the client.
+   - Add the routing for the two networks.
+   - If necessary, activate NAT on the private interface of the gate.

The setup is started from gateA in netA.

# Connect from gateA to gateB

Connection is started from gateA and commands are executed on gateB.
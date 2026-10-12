```
IPADDR=192.168.20.2
MYPORT=7777
ME=34.56.78.90:7777
PTPADDR=192.168.10.1
PEER=12.34.57.78:7777
```

The settings above show that the connection type is CIPe and the interface name is cipcbo. The interface is started at boot time (ONBOOT=yes). The IP addresses for the CIPe tunnel you create are 192.168.20.2 (on your side) and 192.168.10.1 (on the remote side). Notice that these are private IP addresses representing different networks (192.168.20 and 192.168.10). (Don't use public IP addresses for IPADDR or PTPADDR!)

The PEER value indicates that the remote peer will connect to you from IP address 12.34.56.78 on port number 7777. The ME value identifies the IP address of your real connection to the Internet. Replace 12.34.56.78 and 34.56.78.90 with the real, public IP address of the remote peer and your local computer, respectively! The port numbers can be any unused UDP ports you choose. They don't have to be the same (though they are here), but each side does need to know which ports the other side is using.

Although once the other side is up, you should be able to ping each other across the connection, to make the connection useful, you may need to do some additional work:

+   - **Turn on IP forwarding.** If you want the remote CIPe to forward requests to other interfaces on your computer (permanently), add this to the `/etc/sysctl.conf` file:

```
net.ipv4.ip_forward = 1
```

To have IP forwarding take effect immediately, type the following as root user:

```
# echo 1 > /proc/sys/net/ipv4
```

+   - **Open your firewall for CIPe.** At the very least, you need to allow the remote CIPe peer to connect to your UDP port. In our case, we need to open port 7777 on your external LAN interface (for our example, we used 34.56.78.90, although yours will be different).

+   - **Add routes.** Edit the `/etc/cipe/ip-up` script to include the routes to connect the subnetworks on each side of the connection. For our example, I added the following route so that I could address any computer on the remote LAN (192.168.10.0) from my local CIPe connection:

```
route add -net 192.168.10.0 netmask 255.255.255.0 gw $5
```

+   - **Other ciped options.** You can add options to the `/etc/cipe/options.cipcbo` file to pass to the `ciped-cb` daemon. To see available options, type `info cipe`. Then scroll down and select Parameter List to see a list of all parameters you can set for the daemon. (The `options.cipcbo` file is where the link key is stored, so to use a new key you can change it here. Be sure to keep it protected from access by anyone but root!)
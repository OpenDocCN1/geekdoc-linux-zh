
## Why?

Control. Security. Watchfulness.

- **Control** When you are using a Linux box to connect your internal network to another network (say, the Internet), you have an opportunity to allow certain types of traffic and disallow others. For example, the header of a packet contains the destination address of the packet, so you can prevent packets from going to a certain part of the outside network. For example, I use Netscape to access the Dilbert archives. There are advertisements from doubleclick.net on the page, and Netscape wastes my time by cheerfully downloading them. Telling the packet filter not to allow any packets to or from the addresses owned by doubleclick.net solves that problem (there are better ways of doing this though).

- **Security** When your Linux box is the only thing between the chaos of the Internet and your nice, orderly network, it's nice to know you can restrict what comes tromping in your door. For example, you might allow anything to go out from your network, but you might be worried about the well-known “Ping of Death” coming in from malicious outsiders. As another example, you might not want outsiders telnetting to your Linux box, even though all your accounts have passwords; maybe you want (like most people) to be an observer on the Internet and not a server (willing or otherwise). To do this, simply don't let anyone connect in, by having the packet filter reject incoming packets used to set up connections.

- **Watchfulness** Sometimes a badly configured machine on the local network will decide to spew packets to the outside world. It's nice to tell the packet filter to let you know if anything abnormal occurs; maybe you can do something about it or maybe you're just curious by nature.

## How?

### A Kernel with Packet Filtering

You need a kernel that has the new IP firewall chains in it. You can tell if the kernel you are running right now has this installed by looking for the file /proc/net/ipfwchains. If it exists, you're in.

If not, you need to make a kernel that has IP firewall chains. First, download the source to the kernel you want. If you have a kernel numbered 2.1.102 or higher, you won’t need to patch it (it’s in the mainstream kernel now). Otherwise, apply the patch from the Web page listed previously and set the configuration as detailed below. If you don’t know how to do this, don’t panic; read the Kernel-HOWTO.

The configuration options you will need to set for the 2.0-series kernel are:

```
CONFIG_EXPERIMENTAL=y
CONFIG_FIREWALL=y
CONFIG_IP_FIREWALL=y
CONFIG_IP_FIREWALL_CHAINS=y
```

For the 2.1 or 2.2 series kernels:

```
CONFIG_FIREWALL=y
CONFIG_IP_FIREWALL=y
```

The tool ipchains talks to the kernel and tells it what packets to filter. Unless you are a programmer, or overly curious, this is how you will control the packet filtering.

# ipchains

This tool replaces ipfwadm, which was used for the old IP Firewall code. The package also contains a shell script called ipfwadm-wrapper that allows you to do packet filtering as it was done before. You should not use this script unless you want a quick way of upgrading a system that uses ipfwadm (it’s slower, doesn’t check arguments, and so on). In that case, you don’t need this HOWTO much either. See the “Differences between ipchains and ipfwadm” sections later in this chapter for more details on ipfwadm issues.

# I’m Confused! Routing, Masquerading, Portforwarding, Automatic FW…

This HOWTO is about packet filtering. This means deciding whether a packet should be allowed to pass or not. However, Linux being the hacker’s playground that it is, you probably want to do more than that.

One problem is that the same tool (ipchains) is used to control both masquerading and transparent proxying, although these are notionally separate from packet filtering. (The current Linux implementation blurs these together unnaturally, leaving the impression that they are closely related.)

Masquerading and proxying are covered by separate HOWTOs, and the auto forwarding and port forwarding features are controlled by separate tools, but since so many people keep asking me about it, I’ll include a set of common scenarios and indicate when each one should be applied. The security merits of each setup will not be discussed here.

# Rusty’s Three-Line Guide to Masquerading

This assumes that your external interface is called ppp0. Use ifconfig to find out and adjust to taste.

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
# ipchains -P forward -j DENY
# ipchains -A forward -i ppp0 -j MASQ
```

# Gratuitous Promotion: WatchGuard Rules

You can buy off-the-shelf firewalls. An excellent one is WatchGuard’s FireBox. It’s excellent because I like it, it’s secure, it’s Linux-based, and because they are funding the maintenance of ipchains as well as the new firewalling code (aimed for 2.3). In short, WatchGuard is paying for me to eat while I work for you. So please consider their stuff. Watchguard’s URL is: http://www.watchguard.com.

# Common Firewall-like Setups

You run littlecorp.com. You have an internal network and a single dialup (PPP) connection to the Internet (firewall.littlecorp.com, which is 1.2.3.4). You run ethernet on your local network, and your personal machine is called “myhost”.

# Private Network: Traditional Proxies

In this scenario, packets from the private network never traverse the Internet, and vice versa. The IP addresses of the private network should be assigned from the RFC1597 Private Network Allocations (i.e., 10.*.*, 172.16.*.* or 192.168.*.*).

# IP Chains

The only way things ever connect to the Internet is by connecting to the firewall, which is the only machine on both networks that connects onward. You run a program (on the firewall) called a proxy to do this (there are proxies for FTP, Web access, telnet, RealAudio, Usenet News and other services). See the Firewall HOWTO.

Any services you wish the Internet to access must be on the firewall. (But see the “Limited Internal Services” section later in this chapter.)

Example: Allowing Web access from private networks to the Internet.

- The private network is assigned 192.168.1.* addresses, with myhost being 192.168.1.100 and the firewall's ethernet interface being assigned 192.168.1.1.
- A Web proxy (for example, “squid”) is installed and configured on the firewall, running on, say, port 8080.
- Netscape on the private network is configured to use the firewall port 8080 as a proxy.
- DNS does not need to be configured on the private network.
- DNS does need to be configured on the firewall.
- No default route (aka gateway) needs to be configured on the private network.

Netscape on myhost reads `http://slashdot.org`.

1. Netscape connects to the firewall port 8080, using port 1050 on myhost. It asks for the Web page of `http://slashdot.org`.
2. The proxy looks up the name `slashdot.org`, and gets 207.218.152.131. It then opens a connection to that IP address (using port 1025 on the firewall's external interface) and asks the Web server (port 80) for the Web page.
3. As it receives the Web page from its connection to the Web server, it copies the data to the connection from Netscape.
4. Netscape renders the page.

From `slashdot.org`'s point of view, the connection is made from 1.2.3.4 (firewall's PPP interface) port 1025 to 207.218.152.131 (`slashdot.org`) port 80. From myhost's point of view, the connection is made from 192.168.1.100 (myhost) port 1050, to 192.168.1.1 (firewall's ethernet interface) port 8080.

![](img/a3584dae761d2e3abed8bf40d7637389_544_0.png)

# Private Network: Transparent Proxies

In this scenario, packets from the private network never traverse the Internet, and vice versa. The IP addresses of the private network should be assigned from the RFC1597 Private Network Allocations (i.e., `10.*.*.*`, `172.16.*.*` or `192.168.*.*`).

The only way things ever connect to the Internet is by connecting to the firewall, which is the only machine on both networks that connects outward. You run a program (on the firewall) called a transparent proxy to do this; the kernel sends outgoing packets to the transparent proxy instead of sending them onward (that is, it bastardizes routing).

Transparent proxying means that the clients don’t need to know there is a proxy involved.

Any services you wish the Internet to access must be on the firewall. (But see the “Limited Internal Services” section later in this chapter.)

Example: Allowing Web access from private network to the Internet.

1. The private network is assigned 192.168.1.* addresses, with `myhost` being 192.168.1.100 and the firewall’s ethernet interface being assigned 192.168.1.1.
2. A transparent Web proxy (I believe there are patches for squid to allow it to operate in this manner, or try “`transproxy`”) is installed and configured on the firewall, running on, say, port `8080`.
3. The kernel is told to redirect connections to port 80 to the proxy, using `ipchains`.
4. Netscape on the private network is configured to connect directly.
5. DNS needs to be configured on the private network (that is, you need to run a DNS server as a proxy on the firewall).
6. The default route (aka gateway) needs to be configured on the private network to send packets to the firewall.

Netscape on `myhost` reads `http://slashdot.org`.

1. Netscape looks up the name `slashdot.org` and gets 207.218.152.151. It then opens a connection to that IP address, using local port 1050, and asks the Web server (port 80) for the Web page.

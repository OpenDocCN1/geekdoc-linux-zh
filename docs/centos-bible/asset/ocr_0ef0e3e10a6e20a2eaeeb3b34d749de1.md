as eth0, ppp0, or slp0, to identify the route to the Internet or other outside network. For SNAT you must also identify the actual IP address of the interface. Here is an example of a MASQUERADE rule:

```
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

Here is an example of a SNAT rule:

```
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source 12.12.12.12
```

You can add several source addresses if you have multiple addresses that provide a route to the Internet (e.g., --to-source 12.12.12.12,12.12.12.12,5254). Although MASQUERADE uses some additional overhead, you probably need to use it instead of SNAT if you have a dial-up or other Internet connection for which the IP address changes on each connection.

Remember that you need to make sure that IP forwarding is turned on in the kernel. It is off by default. To turn it on permanently, edit the /etc/sysctl.conf file as described earlier. To turn it on temporarily, you can do the following:

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

In common cases in which you don't know the IP address when you first establish the connection to the Internet through a dial-up, DSL, or cable modem connection, and you require dynamic IP addressing, turn on that service:

```
# echo 1 > /proc/sys/net/ipv4/ip_dynaddr
```

# ### Using iptables as a Transparent Proxy

With the REDIRECT target, you can cause traffic for a specific port on the firewall computer to be directed to a different one. Using this feature, you can direct host computers on your local LAN to a proxy service on your firewall computer without those hosts knowing it.

The following is an example of a set of command-line options to the iptables command that causes a request for Web Service (port 80) to be directed to a proxy service (port 3128):

```
# iptables -t nat -A PREROUTING -t pcp --dport 80 -j REDIRECT --to-ports 3128
```

You can use REDIRECT targets in PREROUTING and OUTPUT chains only within a nat table. You can also give a range of port numbers to spread the re-direction across multiple port numbers.

# ### Using iptables to Do Port Forwarding

What if you have only one static IP address, but you want to use a computer other than your firewall computer to provide Web, FTP, DNS, or some other service? You can use the Destina-
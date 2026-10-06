# Part III: Administering Fedora and RHEL

You can add several source addresses if you have multiple addresses that provide a route to the Internet (for example, --to-source 12.12.12.12.1-12.12.12.12.254). Although MASQUERADE uses some overhead, you probably need to use instead of SNAT if you have a dial-up or other connection for which the IP address changes on each connection.

Remember to make sure that IP forwarding is turned on in the kernel (It is off by default). To turn it on, edit the /etc/sysctl.conf file as described earlier. To turn it off temporarily, you can do the following:

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

If you require dynamic IP addressing (in common cases where you don't know the IP address when you first establish the connection to the Internet through a dial-up, DSL, or cable modem connection), turn on that service:

```
# echo 1 > /proc/sys/net/ipv4/ip_dynaddr
```

# Using iptables as a transparent proxy

With the REDIRECT target you can cause traffic for a specific port on the firewall to be directed to a different one. This feature can direct host computers on your local LAN to a proxy service on your firewall without those hosts knowing.

The following is an example of a set of command-line options to the iptables command that causes a request for Web service (port 80) to be directed to a proxy server (port 3128):

```
-t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 3128
```

You can use REDIRECT targets in PREROUTING and OUTPUT chains only within a nat table. You can also give a range of ports to number the redirection across multiple port numbers.

# Using iptables to do port forwarding

What if you have one static IP address, but you want to use a computer other than your firewall to provide Web, FTP, DNS, or some other service? You can use the Destination Network Address Translation (DNAT) feature to direct traffic for a particular port on your firewall to another computer.

For example, if you want all requests for Web service (port 80) that are directed to the firewall computer (-d 15.15.15.15) to be directed to another computer on your LAN (such as 10.0.0.25), you can use the following iptables command:

```
# iptables -t nat -A PREROUTING -p tcp -d 15.15.15.15 --dport 80 \ 
-j DNAT --to-destination 10.0.0.25
```

(Note that the preceding example should actually appear on one line. The backslash indicates continuation on the next line.)
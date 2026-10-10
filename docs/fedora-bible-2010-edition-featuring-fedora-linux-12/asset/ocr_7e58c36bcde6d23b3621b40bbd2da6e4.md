Remember that you need to make sure that IP forwarding is turned on in the kernel. (It is off by default.) To turn it on permanently, edit the `/etc/sysctl.conf` file as described earlier. To turn it on temporarily, you can do the following:

```
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

If you require dynamic IP addressing (in common cases where you don’t know the IP address when you first establish the connection to the Internet through a dial-up, DSL, or cable modem connection), turn on that service:

```
# echo 1 > /proc/sys/net/ipv4/ip_dynaddr
```

# Using iptables as a transparent proxy

With the REDIRECT target you can cause traffic for a specific port on the firewall computer to be directed to a different one. Using this feature you can direct host computers on your local LAN to a proxy service on your firewall computer without those hosts knowing it.

The following is an example of a set of command-line options to the iptables command that causes a request for Web service (port 80) to be directed to a proxy service (port 3128):

```
-t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 3128
```

You can use REDIRECT targets in PREROUTING and OUTPUT chains only within a nat table. You can also give a range of port numbers to spread the redirection across multiple port numbers. (See the online documentation (type man iptables) for more on this.)

# Using iptables to do port forwarding

What if you have only one static IP address, but you want to use a computer other than your firewall computer to provide Web, FTP, DNS, or some other service? You can use the Destination Network Address Translation (DNAT) feature to direct traffic for a particular port on your firewall to another computer:

For example, if you want all requests for Web service (port 80) that are directed to the firewall computer (-d 15.15.15.15) to be directed to another computer on your LAN (such as 10.0.0.25), you can use the following iptables command:

```
# iptables -t nat -A PREROUTING -p tcp -d 15.15.15.15 --dport 80 \
                -j DNAT --to-destination 10.0.0.25
```

(Note that the preceding example should actually appear on one line. The backslash indicates continuation on the next line.)

You can also spread the load for the service you are forwarding by providing a range of IP addresses (for example, --to-destination 10.0.0.1-10.0.0.25). Likewise, you can direct the request to a range of ports as well.

# Part III: Administering Fedora and RHEL

You can add several source addresses if you have multiple addresses that provide a route to the Internet (for example, --to-source 12.12.12.12-12.12.12.254). Although MASQUERADE uses some overhead, you probably need to use MASQUERADE instead of SNAT if you have a dial-up or other connection for which the IP address changes on each connection.

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

# Chapter 14: Computer Security Issues

You can also spread the load for the service you are forwarding by providing a range of IP addresses (for example, --to-destination 10.0.0.1-10.0.0.25). Likewise, you can direct the request to a range of ports as well.

# Using with iptables

Using the LOG target you can log information about packets that meet the criteria you choose. In particular you might want to use this feature to log packets that seem like they might be improper in some way. If you don't want to drop a packet for some reason, you can just log its activity and decide later if something needs to be corrected.

The LOG directs info to the standard tools used to do logging in Fedora: dmesg and rsyslog. Here's an example of how to use a LOG target:

```
-A FORWARD -p tcp -j LOG --log-level info
```

Instead of info, you could use any of the following log levels available with rsyslog: emerg, alert, crit, err, warn, notice, info, or debug. Using the --logprefix option, you could also add information to the front of all messages produced from this logging:

```
-A FORWARD -p tcp -j LOG --log-level info --log-prefix "Forward INFO"
```

# Enhancing your iptables firewall

You can modify or expand the iptables examples given in this chapter in many ways. iptables is tremendously flexible.

When you create your iptables firewall, you should refer to the iptables man (type man iptables) for detailed descriptions of options, ways of matching, ways of entering addresses, and other details. I also recommend an excellent iptables Tutorial by Andreasson (http://iptables-tutorial.frozentux.net).

Here are a few tips for using iptables features:

- Reduce rules — Try to improve performance by reducing the number of rules. Using chains can keep a packet from seeing rules that don't apply to it.
- Deal with fragments — Use the -f option to refer to the second and subsequent packets of a packet that was split into fragments. In general, it is safe to not drop and third fragments for which you don't have a first packet fragment they won't be reassembled. If you use NAT, the fragments are assembled before filtering, so you shouldn't have problems with unfiltered fragments sent through.
- Opposite — To make a rule its opposite, use an exclamation mark (!).
- All interfaces — To match all interfaces of a type, use a plus sign (+), as in eth+.
- Blocking connections — Use the --syn option to block SYN packets (that, those packets requesting connections). This applies only to TCP packets.
- Limiting — Use the --limit option to restrict the rate of matches that result in log messages. This option allows matches to produce messages only a limited number of times per second (the default is three with bursts of five).
- Denial of Service (DOS) Attacks — You can use the --limit option to reduce the impact of DOS attacks, but it won't stop them altogether. As long as the traffic is directed at your server, your bandwidth is being leeched away, and the machine utilizes resources to ignore the data.
- Table types — The default table type is filter. The other types tables are nat (for masquerading) and mangle (for altering packets). To use a table other than filter you must add -t table_type where table_type is either nat or mangle.

# Controlling Access to Services with Wrappers

Completely disabling an unused service is fine, but what about the access to services that you need? How can you selectively grant or deny these services? In previous versions of Red Hat Linux, the tcp wrapper daemon (tcpd) was used to facilitate this for login, telnet, finger, and talk. TCP wrappers are also enabled for other services such as vsftp. When a service relies on TCP wrappers, the hosts.allow and hosts.deny files are scanned and checked for the IP address of the connecting machine. These checks are made when connection occurs:

- If the address is listed in hosts.allow file, the connection is allowed and hosts.deny is not checked.
- If the address is in hosts.deny (but not the hosts.allow file), the connection is denied.
- If the address is in neither file, the connection is allowed.

It is not necessary (or even possible) to list every address that may connect to your computer. The hosts.allow and hosts.deny files enable you to specify subnets and groups of addresses. You can even use the keyword ALL to specify all addresses. You can restrict specific entries in these files apply only to specific network. Look at an example of a typical pair of hosts.allow and hosts.deny. Here's the /etc/hosts.allow file:

```
# hosts.allow describes the names of the hosts which are allowed to use the local INET services, as decided by /usr/sbin/tcpd server.
cups-lpd: 199.170.177.in.telnetd: 199.170.177.linuxtoys.net
vsftpd: ALL
```

Here's the /etc/hosts.deny file:

```
# hosts.deny describes the names of the hosts which are not allowed to use the local INET services, as decided by /usr/sbin/tcpd server.
ALL: ALL
```

The preceding example is a rather restrictive configuration. It allows connections to the cups-pd and telnet services from certain hosts, but then denies all connections. It also allows connections to the FTP service (vsftp) to all hosts. Let's examine the files in detail.

As usual, lines with a # character are ignored by xinetd when it traverses the file. Each noncomment line consists of a comma-separated list of daemons followed by a colon (:) character and a comma-separated list of addresses to check. In this content, a client that attempts to access a network service on your system a client entry can be a numeric IP (such as 199.170.275) or a hostname (such as jukebox.linuxtoys.net), but more often a wildcard that specifies an entire range of addresses. A client entry can take four different forms. The online manual page of the hosts.allow file describes them as follows:

- A string with a dot (.) character. A hostname is matched if the last components of its name match the specified pattern. For example, the pattern .tue.nl matches the hostname www.vin.tue.nl.
- A string that ends with a dot (.) character. A host is matched if its first numeric fields match the given string. For example, the pattern 131.155 matches the address of most every over the Eindhoven University network (131.155.x.x).
- A string that begins with an @ symbol is treated as an NIS group name. A hostname is matched if it is a host member of the specified network. Netgroup matches is not supported for daemon process names or for client users.
- An expression of the form n.n.n.n/m.m is interpreted as a net/mask pair. A host address is matched if net is equal to the bitwise and of the address and the mask. For example, the net/mask 131.155.72.0/255.255.254.0 matches every address in the range 131.155.72.0 through 131.155.73.255.

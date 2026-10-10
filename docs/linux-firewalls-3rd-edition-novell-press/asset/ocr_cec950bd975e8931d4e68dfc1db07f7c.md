The **ntpd** startup script that is run at boot time uses **ntpd** to query a series of public time service providers. The ntpd daemon is started after the server's reply. These hosts would be individually specified in a series of firewall rules:

```
TIME_SERVER="my.time.server"   # external time server, if any
if [ "$CONNECTION_TRACKING" = "1" ]; then
$IPT -A OUTPUT -o $INTERNET -p udp \
    -s $IPADDR --sport SUNPRIVPORTS \
    -d $TIME_SERVER --dport 123 \
    -m state --state NEW -j ACCEPT
fi
$IPT -A OUTPUT -o $INTERNET -p udp \
    -s $IPADDR --sport SUNPRIVPORTS \
    -d $TIME_SERVER --dport 123 -j ACCEPT
$IPT -A INPUT -i $INTERNET -p udp \
    -s $TIME_SERVER --sport 123 \
    -d $IPADDR --dport SUNPRIVPORTS -j ACCEPT
```

Note that the previous rules are written for a standard client/server UDP communication. Depending on your particular client and server software, it's possible that one or both of them will use the NTP server-to-server communication model, with both the client and the server using UDP port 123.

# # Filtering ICMP Control and Status Messages

ICMP control messages are generated in response to a number of error conditions, and they are produced by network analysis programs such as **ping** and **traceroute**.

> **ICMP MESSAGE TYPES AND IPTABLES**
> iptables supports the use of either the ICMP numeric message type or the alphabetic symbolic name.
> iptables also supports use of the message subtypes, or codes. This is especially useful for finer filtering control over type 3 Destination Unreachable messages. For example, you could specifically disallow outgoing Port Unreachable messages to disable an incoming traceroute, or you could specifically allow only outgoing Fragmentation Needed messages.
> To see a list of all supported ICMP symbolic names in iptables, run `iptables -p icmp -h`. To see the official RFC assignments, go to [http://www.iana.org/assignments/icmp-parameters](http://www.iana.org/assignments/icmp-parameters).
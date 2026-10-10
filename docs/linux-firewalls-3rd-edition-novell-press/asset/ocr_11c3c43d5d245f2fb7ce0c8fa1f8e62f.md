default limit is three matches per hour. Optional time frame specifiers include /second, /minute, /hour, and /day.

In other words, by default, when the initial burst rate of five matches is reached within the time limit, at most three more packets will match over the next hour, one every 20 minutes, regardless of how many packets are received. If a match doesn’t occur within the rate limit, the burst is recharged by one.

It’s easier to demonstrate rate-limited matching than it is to describe it in words. The following rule will limit logging of incoming ping message matches to one per second when an initial five echo-requests are received within a given second:

```
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request \
-m limit --limit 1/second -j LOG
```

It’s also possible to do rate-limited packet acceptance. The following two rules, in combination, will limit acceptance of incoming ping messages to one per second when an initial five echo-requests are received within a given second:

```
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request \
-m limit --limit 1/second -j ACCEPT
iptables -A INPUT -i eth0 \
-p icmp --icmp-type echo-request -j DROP
```

The next rule limits the number of log messages generated in response to dropped ICMP redirect messages. When an initial five messages have been logged within a 20-minute time frame, at most three more log messages will be generated over the next hour, one every 20 minutes:

```
iptables -A INPUT -i eth0 \
-p icmp --icmp-type redirect \
-m limit -j LOG
```

The assumption in the final example is that the default and any additional unmatched redirect packets are silently dropped by the default DROP policy for the INPUT chain.

# dstlimit filter TABLE MATCH EXTENSION

The dstlimit match extension enables rate limiting on a per-destination basis, whether per IP address or per port. Note the difference between the dstlimit match extension and the limit match extension, which has one limit for packets of a certain type.

Table 3.14 lists the options for the dstlimit match extension.
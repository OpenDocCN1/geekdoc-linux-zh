Table 4.9 ping command options (continued)
| Option | Description |
| :--- | :--- |
| `-Q` | Quiet mode |
| `-R` | Toggle record route option |
| `-S` | Specifies the number of bytes to be sent with each request |

# Determining Network Performance

The **ping** command can be used to measure the amount of time required to transmit a message to a remote destination and the time required to obtain a response. This use of the **ping** command in essence measures the relative performance of the path between the two devices at a given point in time. It does not, by any means, provide a detailed analysis of the devices or connectivity between them. Rather, it provides a glimpse of the general condition of the path at the point it is measured. It could be said that network performance is like the stock market. One day it is up and the next it is down. The primary difference with respect to volatility is whether we are talking in terms of days or milliseconds. A large number of factors can cause network performance to vary. These include users that are overly aggressive about using network resources, hardware problems, software configuration problems, and so forth.

The **ping** command provides a means of determining system response times as well, but it takes a little more work to determine if the observed performance problem is related to a specific slow system or a delay in some other network component. The **ping** tool shows output that can be used to measure and report round-trip time and provide packet-loss statistics. By default, **ping** issues an ICMP request every second to the destination supplied on the command line and reports the status of each ICMP reply. Sample output includes the following:

```
# ping didymus
PING didymus-gw2.home.com (10.0.2.127): 56 data bytes
```

(continued)
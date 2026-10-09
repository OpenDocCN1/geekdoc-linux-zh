The best source of time servers is the list at *http://www.pool.ntp.org/*. This group has collected public NTP servers into round-robin DNS pools, allowing easy NTP configuration. These NTP servers are arranged first in a global list, then by continent, and then by country. For example, if you're in Canada, a brief search on that site leads you to *0.ca.pool.ntp.org*, *1.ca.pool.ntp.org*, and *2.ca.pool.ntp.org*. We'll use these servers in the following examples, but look up the proper servers for your country and use those instead when setting up your own time service.

# ## Configuring ntpd(8)

ntpd(8) checks the system clock against a list of time servers. It takes a reasonable average of the times provided by the time servers, discarding any servers too far away from the consensus, and gradually adjusts the system time to match the average. This gives the most accurate system time possible, without demanding too much from any one server, and helps keep errant hardware in check. Configure NTP in */etc/ntpd.conf*. Here's a sample that uses Canadian time servers:

```
```text
server 1.ca.pool.ntp.org
server 2.ca.pool.ntp.org
server 3.ca.pool.ntp.org
```
```

This system checks three time servers for updates. If you list only one server, ntpd(8) slaves its clock to that one server and shares any time problems that server experiences. Using two time servers guarantees that your system won't know what time it is; remember, NTP takes an average of its time servers but throws out any values too far out of range of the others. How can NTP decide whether one server is wrong when it has only two values to choose from? Using three time servers is optimal; if one server runs amok, ntpd recognizes that the time offered by that server doesn't make sense against the time offered by the other two servers. (Think of this as a “tyranny of the majority”; the one guy whose opinion differs from the rest doesn't get any voice at all.)

# ## ntpd(8) at Boot Time
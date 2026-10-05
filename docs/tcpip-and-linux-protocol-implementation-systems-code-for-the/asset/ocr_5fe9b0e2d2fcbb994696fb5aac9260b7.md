# 874 TCP/IP and Linux Protocol Implementation

and maximum threshold and average number of packets in the queue that trigger and set the drop (or marking) probability (marking if ECN is set).

gred. GRED includes a range of drop probabilities suitable, for example, for the differentiated services AF class.

```
gred DP drop-probability limit <bytes> min <bytes> max
<bytes> avpkt <bytes> burst <n pkts> probability <prob>
bandwidth <kbps> grep [prio value] grep setup DPs <no. of
DPs default [default DP] [gric]
```

dsmark. Differentiated services marking involves up a set of indices to a set of mask/value pairs.

```
dsmark indices <indices> [ default index <default index> /
[ set_tc_index ]
```

ingress. Takes an IP address as a parameter. tc qdisc list will show the current set of queuing disciplines instantiated.

# TC Class Command

```
tc class [ add | del | change | get ] dev <string>
[ classic <class id> ] [ root | parent <class id> ]
[[ <disc kind> ] [ help | <options> ] ]
```

Essentially, class identifiers are attached to queuing disciplines, and are either a root, or are attached to parent classes. A class can also have an estimator attached.

# TC Filter Command

```
tc filter show [ dev <string> ] [ root | parent <class id> ]
```

Where:

```
FILTER_TYPE := { ravp | u32 | fw | route | etc. }
FILTERID := ... format depends on classifier, see there
OPTIONS := ... try tc filter add <desired FILTER_KIND> help
```
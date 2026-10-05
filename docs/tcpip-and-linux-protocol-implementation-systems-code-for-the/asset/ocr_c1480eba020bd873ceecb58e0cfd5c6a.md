# 9.14.3 TC Command Usage

The tc command usage is fairly complex, since there are three intertwined types of object one can set up. As described earlier, we have a filter type, a class, and then the actual queuing discipline with its parameters. Normally, one uses tc to select a queuing discipline for a device, then attaches a filter to the device to direct packets to the appropriate queue. In more complex cases, this recurses via CBQ or CSZ and the use of class identifiers, as well as filters.

```
tc [ OPTIONS ] OBJECT { COMMAND | help \
where OBJECT := \ qdisc | class | filter \\}
OPTIONS := \ -[tatistics] | -d[etails] | -r[aw] }
```

# TC Qdisc Command

As discussed in the rest of this chapter, the queuing discipline is currently one of { atm | [p|b]fifo | tbf | prio | hfsc | hpfq | sfq | cbq | csz | red | gred | ingress | etc. }

```
tc qdisc [ add | del | replace | change | get ] dev STRING
[ HANDLE ] [ root | ingress | parent CLASSID ]
[ estimator INTERVAL TIME_CONSTANT ]
[ QDISC_KIND ] [ help | OPTIONS ] }
```

We can add a base queue discipline optionally with a handle, or as a child in a class hierarchy (usually previously defined by CBQ or CSZ), or we can be an estimator. One exceptional case is ingress queuing.

The estimator takes an interval and a time constant over which the estimate decays. This is used to monitor queue occupancy, without running too many cycles while doing so.

When we add or modify a given queuing discipline, there are configuration parameters we must also set up. The options each queuing discipline can be configured with (roughly) as follows:

atm. IP over ATM can set up parameters as part of a class hierarchy. These include the type of ATM VC in use, and the VC class (in the ATM sense, in other words, UBR, VBR, and so on). The ATM AAL-level parameters such as SDU (packet size, 9,280 bytes), and any ATM-level addressing information (e.g., whether E164 or ISO addresses are used to identify the link layer next hop address, or in other words the ATM VC end point).
# 20.1.4 Configuration Files for gated

As mentioned earlier, each member's aliasd daemon (part of the cluster alias component discussed in Chapter 16) will create a member-specific gated.conf file (not a CDS L) named /etc/gated.conf.membern (with the "n" replaced by a member number). The following example shows the member-specific gated.conf file. (For more information on the syntax of this file, see the following reference pages: gated.conf(4), gated.control(4), gated.proto(4), gated_intro(4)).

```
# cd /etc && file gated*

gated.conf: symbolic link to ../../cluster/members/(memb)/etc/gated.conf
gated.conf.default: c program text
gated.conf.member1: c program text
gated.conf.member2: c program text
```

```
# cat /etc/gated.conf.member1
# This file created automatically by "aliasd", DO NOT EDIT!
#

traceoptions "/usr/tmp/gated.log" replace size 1000k files 2 general;
# any dead interfaces will be entered here with a high (i.e. undesireable)
# preference, so that gated will be compelled to put a better route
# in the kernel forwarding table

interfaces {
    interface all passive;
};
# broadcast routes with RIP if at least one interface is healthy
# make a default route through the cluster interconnect look expensive
# If an interface has been marked as "dead" by NIFF then we
# will also exclude RIP routes via the affected interface.
# This closes a hole where gated doesn't qualify the interfaces
# over which it hears broadcasts, and will possibly install a route
# through a dead interface.
#
# Lastly, we place a catch-all "all nripin noripout" here so that
# if an interface is brought on-line after aliasd has started, it
# won't automatically get used by gated.
#
rip yes {
    broadcast;
    interface ics0 ripin ripout metricout 10;
    interface tu0 ripin ripout metricout 10;
    interface tu1 ripin ripout;
    interface all noripin noripout;
};
```
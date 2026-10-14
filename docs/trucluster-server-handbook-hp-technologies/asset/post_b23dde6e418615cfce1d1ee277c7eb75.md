
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

```
# one "host" or network number per alias
#
# alias will also reroute direct routes for interfaces
# marked as "dead" by NIF by inserting a new gateway
# for that route here
#
```

Note, the next few lines describe the default cluster alias.

```
static {
    host 192.168.0.70 interface 127.0.0.1;
};

# arrange to export alias host/network routes:
#
# o don't publish routes learned through RIP
# o publish the "static" routes given above, except for
#   ophaned networks that we're routing around
# o publish direct routes for virtual subnets which have real
#   interfaces attached to them
#
# for the cluster interconnect, arrange to broadcast a
# high-cost default route over it
#
# this default may have been learned from RIP (proto rip)
# or it may have been statically configured (proto kernel)
# we give a slight advantage to a default route via RIP
```

Note, the next few lines describe the Cluster Interconnect (CI) virtual address.

```
export proto rip interface 10.0.0.1 {
    proto rip {
        default;
    };
    proto kernel {
        default metric 3;
    };
};
```

Note, the next few lines describe the LAN interconnect.

```
export proto rip interface 10.1.0.1 {
    proto rip {
        default;
    };
    proto kernel {
        default metric 3;
    };
};

export proto rip interface 192.168.0.68 {
    proto rip restrict;
};
```

Pretty ugly, huh? You are probably starting to see why HP recommends not setting up your system as an IP router unless you are very experienced with gated and network administration in general. (See the first line of the gated.conf.membern file: “# This file created automatically by "aliasd", DO NOT EDIT!”)

Still want to give it a whirl? Then follow these steps according to the *TruCluster* Server Cluster Administration Guide in the documentation set (Chapter 6): If gated is running, stop it with the following command:

```
`# /sbin/init.d/gateway stop`
```

- 1. Enter the following command:
  
      `# cluamgr -r start,nogated`

- 2. Modify gated.conf (to the name that you are using for the configuration file).
  
  Use the version of `/etc/gated.conf.membern` that was created by the “cluamgr -r nogated,start” command as the basis for edits to a customized gated configuration file. You will need to correctly merge the cluster alias information from the `/etc/gated.conf.membern` file into your customized configuration file.

- 3. Start gated with the following command:
  
      `# /sbin/init.d/gateway start`

In this special case, you will be providing a non-standard configuration file for gated to use (perhaps requiring Open Shortest Path First (OSPF) instead of RIP); therefore, you will need to enter the string “nogated” for CLUA_ROUTE_ARGS in `/etc/rc.config.common` in order to prevent aliasd from restarting gated using the gated.conf.membern file upon reboot.

Retrieve the CLUA_ROUTE_ARGS from the rc.config.common file. We do this to verify that there is not any previous attribute value (and to merge the contents if necessary).

```
`# rcmgr -q get CLUA_ROUTE_ARGS`
```

Add in the new value for the CLUA_ROUTE_ARGS environment variable.

```
`# rcmgr -s set CLUA_ROUTE_ARGS "nogated"`
```

## NOTE:

Do not place the CLUA_ROUTE_ARGS environment variable in a member-specific `rc.config` file.

# 734 Linux Administration: A Beginner's Guide

| Option | Description |
| --- | --- |
| -p | Specifies a different User Datagram Protocol (UDP) port for the DHCP client to use instead the standard port 68 |
| -d | Forces the DHCP client to run as a foreground process instead of its normal behavior of running as a background process; useful for debugging |

Table 29-2 dhclient Command-Line Options

body, the client daemon can be started with additional flags that slightly modify the behavior of the application. For example, you can optionally specify the interface (such as eth0) for which address lease should be requested. Some of the options for dhclient are described in Table 29-2. The full syntax of the dhclient command is shown here:

```
Usage: dhclient [-4] [-6] [-SWPT1dvrxi] [-nw] [-p <port>] [-D LL|LLT]
[-s server-addr] [-cf config-file]
[-df duid-file] [-lf lease-file]
[-pf pid-file] [-no-pid] [-e VAR=val]
[-sf script-file] [interface]
```

# Summary

DHCP is a useful tool for dynamically configuring the addresses for large groups of machines or mobile workstations. Since DHCP is an open and standards-based protocol, the architecture and platform of the server and the client are normally irrelevant.
A computer running Linux can serve DHCP requests. The software to do this is highly configurable and has mechanisms to persist after machine failures.

Software also exists to configure the networking stack of a Linux-based machine from a DHCP server on the network. This client daemon has a number of options that make it able to speak to a variety of DHCP servers.
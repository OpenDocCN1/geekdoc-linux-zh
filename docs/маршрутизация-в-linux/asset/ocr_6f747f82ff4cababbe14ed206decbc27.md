+   - **gateway.** The name or IP address for the gateway that traffic must pass through to get to *address*.
+   - **cost.** The RIP cost of going through this gateway, determined according to the rules discussed in Chapter 1.

Passive gateway information is loaded at boot time—when *routed* starts. It is not reloaded unless you restart the routing daemon.

# Running routed

The *routed* daemon, as mentioned earlier, should be set to start at boot time. You do this either through a file, such as rc.local, or by adding an initialization script pointer for the run levels that require the routing daemon. In either case, there are flags available so you can specify particulars about how this program should run. Table 5.1 lists the options and their functions.

Table 5.1 Flags and Options Available for the IPv4 Version of routed

| Option | Result |
|---|---|
| -d | Saves extensive debugging information. |
| -g | Sets a default route, such as -g 192.168.52.1. Typically used to point to external destinations that routed may not be able to find on its own, such as the Internet or a router using another protocol. |
| -s | Supplies routing information even if there is only one network interface, which normally tells routed to assume that it is not an internetwork router. |
| -q | Does not supply routing information even if there are multiple network interfaces. |
| -t | Runs routed linked through the terminal, so packet information is shown on STDOUT and the process can be killed using Ctrl-C. Used for testing purposes. |
| filename | If you end the line with a filename, that file is used to log routed's behavior. |

# Guide to gated

Another program you have heard much about in earlier chapters is gated. There are actually three different versions of this program. You can utilize gated for either unicast or multicast use, for either IPv4 or IPv6, or any combination of these you require—just make sure you have the correct version (see Table 5.2) for each. This routing daemon comes with many versions of Linux, though it might be on a second disk or among supplementary materials. If this is the daemon you decide to use and
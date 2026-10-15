
- **gateway.** The name or IP address for the gateway that traffic must pass through to get to *address*.
- **cost.** The RIP cost of going through this gateway, determined according to the rules discussed in Chapter 1.

Passive gateway information is loaded at boot time—when *routed* starts. It is not reloaded unless you restart the routing daemon.

## Running routed

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

## Guide to gated

Another program you have heard much about in earlier chapters is gated. There are actually three different versions of this program. You can utilize gated for either unicast or multicast use, for either IPv4 or IPv6, or any combination of these you require—just make sure you have the correct version (see Table 5.2) for each. This routing daemon comes with many versions of Linux, though it might be on a second disk or among supplementary materials. If this is the daemon you decide to use and don't have it, want the latest version, or need a capability that didn't come with the version packaged with your distribution, go to www.gated.org or www.gated.merit.edu to obtain them.

### Table 5.2 Versions of gated and Their Capabilities

| Version | Enables |
|---|---|
| gated-ipv6 | Static IPv6 routing, RIPng, and BGP4MP. |
| gated-multicast | IGMP, MP-BGP, MSDP (check to see if this implementation is complete), DVMRP, PIM-SM, and PIM-DM. |
| gated-public | EGP, BGP, RIP-1, RIP-2, and OSPF. The public version is a slightly older but very stable version. |
| gated-unicast | EGP, BGP, RIP-1, RIP-2, OSPF, and Intermediate System to Intermediate System (IS-IS). |

The public version is a slightly older but very stable version. The unicast, multicast, and IPv6 versions are all newer and available through the main site as well. Access to the public version's source code is possible but not to the newer versions unless you obtain a license—if you require source code access, the zebra (http://www.zebra.org) daemon might be a better choice for you.

It is the public version we'll focus on in this chapter.

## How Public gated Works

Like most routing daemons, the gated routing daemon typically starts at boot time—you'll want to be sure that it is set up to do so on the Linux box you use for your router. See the section "Running Public gated" for ideas on using the gdc program to interface with the daemon rather than directly starting it by hand.

When gated starts, it first determines how much space it needs in memory for its arrays and other data structures. After it knows how much room it needs, gated is assigned a virtual machine with a 32-bit address space in either RAM or on a hard drive (this is how Linux handles all processes). The daemon then reserves a section of its space to hold the information and then clears out anything already stored there—a process called initializing memory. After this, it reserves another section of its space for each of the threads it will use to keep track of its state and serve other functions. The gated daemon then creates the memory framework for the data structures, such as routing tables, to which it needs fast access.

After the entire framework is in place, gated reads the kernel's routing tables into its own RAM—something it won't do again unless specifically instructed or restarted. It then finds the interfaces on this specific machine and records both their addresses and whether they are currently up or down.

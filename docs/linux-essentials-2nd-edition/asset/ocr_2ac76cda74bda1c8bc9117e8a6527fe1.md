# # Testing Your Network Connection

In most cases, your network connection will work fine from the moment you start it. At times you may need to diagnose problems, either because you can't get the connection to work at all or because a formerly working connection has stopped working. In the following pages, we describe several types of network tests: checking your routing table, testing basic connectivity, testing to locate where a break in connectivity has occurred, testing DNS functioning, and testing your network's status.

# ## Checking Your Routing Table

Earlier we described using the route command to set the default route on a computer. You can check that your route is sensible by using the same command. In most cases, typing route alone will do the job:

| $ route | | | | | |
| Kernel IP routing table | | Genmask | Flags Metric Ref Use If |
| Destination | --- | --- | --- | --- | --- | --- |
| 192.168.29.0 | * | 255.255.255.0 | U | 0 | 0 | eth0 |
| 127.0.0.0 | | 255.0.0.0 | U | 0 | 0 | eth0 |
| default | 192.168.29.1 0.0.0.0 | UG | 0 | 0 | eth0 |

This shows that data for 192.168.29.0 (that is, any computer with an IP address 192.168.29.1 and 192.168.29.254) goes directly over eth0. The 127.0.0.0 is a special interface that "loops back" to the originating computer. Linux uses this for internal network purposes. The last line shows the default route, which describes what to do with everything that doesn't match any other entry in the routing table. This line identifies the default route's gateway system as 192.168.29.1. If it's missing or misconfigured, or all traffic destined for external networks, such as the Internet, won't make it beyond your local network segment.

# ## Testing Basic Connectivity

The most basic network test is ping, which sends a simple network packet to the system name (via IP address or hostname) and waits for a reply. In Linux, ping continues sending packets every second or until you interrupt it with a Ctrl+C keystroke. You can instead specify a limited number of tests with the - c option. Here's an example of its output:
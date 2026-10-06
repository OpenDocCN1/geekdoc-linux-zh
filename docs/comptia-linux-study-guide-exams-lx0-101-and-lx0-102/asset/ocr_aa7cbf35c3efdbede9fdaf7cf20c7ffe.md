# Diagnosing Network Connections

413

to know the hostnames of problem systems because that can help you pinpoint yours
responsible for a problem.

This sample output shows a great deal of variability in response times. The first hop, to
192.168.1.1, is purely local; this router responded in 1.021, 36.519, and 0.971 milliseconds
(ms) to these probes. (Presumably the second probe caught the system while it was
selecting else.) Probes of most sequences are in the 8–20ms range, although
one is at 103.068ms. The final system has only two times; the probe never returned,
as the asterisk (*) on these lines indicates.

Using traceroute, you can localize problems in network connectivity. Highly variable
times and missing times can indicate a router that is overloaded or has an unreliable
to previous router on the list. If you see a dramatic jump in times, it typically
means the physical distance between routers is greater. This is common in
intercontinental links. Such jumps don't necessarily signify a problem unless the two
systems are close enough that a huge jump isn't expected.

What can you do with the traceroute output? Most immediately, traceroute is helpful
in determining whether a problem in network connectivity exists in a network where
you're responsible. For instance, the variability in the first hop of the preceding example
c indicate a problem on the local network, but the last packet accounted with the final
destination most likely not a problem. If the trouble link is within your jurisdiction,
You can check the status of the system, nearby systems, and the network segment
in general.

> Some routers are configured in a way that traceroute isn't a useful
tool; these block all traceroute data, either to themselves only or
for all packets that pass through them. If your traceroute output contains
one or two lines of asterisks but everything else seems OK, chances are
you've run into such a system. If you see nothing but asterisks after a cer-
t router but diagnostic tools like ping work, a router is probably
blocking all traceroute operations.

![](bbox=[0.147, 0.517, 0.23, 0.555])

The tracepath program is an alternative to traceroute. In operation, it's similar,
although it produces one line of output for each test packet and yields larger outputs
an traceroute. There are fewer traceroute options than there are traceroute
options.

# Checking Network Status

Another useful diagnostic tool is netstat. This is of Swiss Army knife of
network tools because it can be used in place of several others, depending on the parameters
it's passed. It can also return information that's not easily obtained in other ways. Examples
include the following:

Interface Information Pass netstat --interface or -i parameter to obtain
information about your network interfaces similar to what ifconfig runs. (Some)
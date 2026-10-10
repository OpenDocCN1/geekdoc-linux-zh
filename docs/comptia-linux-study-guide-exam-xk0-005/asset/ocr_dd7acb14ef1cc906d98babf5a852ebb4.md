TABLE 20.1 Commands to check for high latency, saturation

| Command | Description |
| --- | --- |
| iperf, iperf3 | Perform network throughput tests. The iperf command is version 2 of the utility, and iperf3 is version 3. |
| iftop -i adapter | Displays network bandwidth usage (throughput) for adapter in a continuous graph format. |
| mtr | Displays approximate travel times and packet loss percentages between the first 10 routers in the path from the source to the destination in a continuous graph or report format. |
| nc | Performs network throughput tests. (Called netcat) |
| netstat -s | Displays summary statistics that are broken down by protocol and contain packet rates, but not throughput. This command is deprecated. |
| ping, ping6 | Perform simple ICMP packet throughput tests and display statistics on items such as round-trip times. |
| ss -s | Displays summary statistics that are broken down by socket type and contain packet rates but not throughput. |
| traceroute, traceroute6 | Display approximate travel times between each router from the source to the destination, discovering the maximum transmission unit (MTU) along the way. |
| traceroute, traceroute6 | Display approximate travel times between each router from the source to the destination. |

> NOTE
> 
> Some of these tools are not installed by default. Also, they may not be in a distribution's standard repositories. See Chapter 13, “Governing Software,” for details on how to install software packages.

To employ the `iperf` utility for testing throughput, you'll need two systems—one to act as the server and the other as a client. The utility must be installed on both systems, and you'll need to allow access to its default port 5001 (port 5201 for iperf3) through their firewalls. A snipped example of setting up and starting the `iperf` server on an Ubuntu system is shown in Listing 20.1.
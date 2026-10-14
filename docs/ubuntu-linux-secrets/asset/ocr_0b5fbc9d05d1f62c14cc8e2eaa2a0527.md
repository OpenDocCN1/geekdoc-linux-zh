The Ping program sends the ICMP requests to the remote host and determines the amount of time it takes for the request to return from the remote host. It creates a graphical histogram of each request time and provides statistics on the minimum, maximum, and average times. Clicking the Details arrow produces a list of the individual test results.

The Ping program is useful in troubleshooting network latency. Network latency is how much delay occurs when sending packets across the network to a specific host. Often you can troubleshoot network routing problems using the Ping program.

> **Secret**
> 
> Many system administrators now consider the Ping program a network vulnerability and block ping requests on their servers. Don’t be too surprised if you try to ping a server and don’t get a response.

# Netstat

The Netstat tab provides information on three sets of network data available on the workstation:

+   - The routing table
+   - The active network services
+   - The multicast network information

Ubuntu maintains an internal routing table to keep track of how to forward network packets to remote networks. Selecting the Routing Table radio button then clicking the Netstat button produces a list similar to the one shown in Figure 14-10.

![](bbox=[0.177, 0.591, 0.614, 0.922])

**Figure 14-10:** The Netstat routing table output.
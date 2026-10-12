# ## 6.9 Lab – complex sub-nets (1) – planning

As an example of how to plan and implement a whole sub-netted internal network for a whole organization, we’re going to sub-net the hypothetical small company that we mentioned in Module 6.6, using the IP address range 192.0.2.0/24. We’ll take it step by step.

+   1. make a list of the separate networks you require
+   	- main network, not part of any sub-net (“HQ machines”)
+   	- human resources department (“HR”)
+   	- operations department (“Ops”)
+   		- operations, sub-net for sales (“Sales”)
+   		- operations, sub-net for technical (“Tech”)
+   	- finance department (“Fin”)
+   2. draw a diagram of the networks (Figure 6.16)

![](bbox=[0.14, 0.37, 0.91, 0.79])

+   3. specify the maximum number of hosts for each network
+   Enter the details as shown in Table 6.1. For each sub-net:
+   
+   - enter only the number of hosts on that network’s own wire; don’t include hosts in its child sub-nets if it has any, and don’t include any routers, because we do that explicitly in a moment
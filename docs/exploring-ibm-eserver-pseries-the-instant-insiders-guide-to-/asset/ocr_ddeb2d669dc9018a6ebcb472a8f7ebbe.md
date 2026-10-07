# Application Programs and Operating Systems 227

the end user would potentially be able to view and interact with an applet by rotating a product image dynamically. Applets can also be created to take advantage of native tools on specific platforms. For example, an applet could be written to specifically interact with a data-base running on AIX 5L to dynamically extract and post information on a user's graphics display such as live weather maps or 10-minutedelayed stock prices. Applets can be discarded easily after they have been run, or they can be saved to media for future. A set of sample applets is included to demonstrate a number of features of Java.

# AIX Workload Manager

AIX Workload Manager (WLM) is a standard feature of AIX 5L and is intended to help system administrators apply resource management policies to different workloads and manage peak demands. This capability can also be used to consolidate workloads from several different systems onto one pSeries system.

The WLM function provides a policy-based method for managing system workload and system resources, including the following:

+   - System resource allocation with fine granularity to specific jobs
- Logical job separation on the server
- Keeping applications in memory for more predictable performance
- Dynamically changing policies as job requirements change
- Control options that include minimum and maximum percentage limits, shares, or a combination of both

As a function of AIX 5L, WLM will operate on any pSeries system from the smallest to the largest. WLM can also be used in LPAR environment. Within each logical partition, the system resources assigned to that LPAR can be allocated to certain applications, just as if the LPAR were an independent server. This feature is extremely useful in guaranteeing proportional or minimal levels of resource to various applications.
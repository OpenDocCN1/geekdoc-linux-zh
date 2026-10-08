# ## Using Network Performance Data

This section provides a brief introduction on how you can use the network performance monitoring tools to detect and address network performance problems. Various types of network performance problems are possible. Potential problems could be an overloaded server, a congested network, or a faulty network masquerading as an overloaded network. You can use the performance tools to avoid these problems, if possible, or at least to correct them quickly when they occur.

# ### Avoiding Performance Issues

To avoid network performance issues, key networks should be monitored regularly to look for trends. You should first use tools such as PerfView and NetMetrix to collect baseline data from when the computing environment is behaving normally. You may want to put some NFS commands into scripts to create your own benchmarks. Be sure that your mixture of NFS commands reflects the typical usage for your environment. In addition to benchmarking utilization rates, you should determine what collision rates are typical by using lanadmin or MeasureWare. Data should be collected over a period of time to get an accurate view of the network load. As loads increase, you should be prepared to segregate network traffic, add more LAN cards, or restrict the number of new applications being used on the network.

Network performance problems can be caused by an increase in the number of users or the introduction of a new application into the production environment. By proactively collecting performance information, you can identify when a jump in usage occurred and you may be able to trace it to a new application or a user’s inappropriate use of the network. Network analyzers and tools such as NetMetrix can be used to identify the applications and users dominating network traffic. A new network application initially should be deployed in a test environment so that its network load can be characterized. If its network usage is unexpectedly high, it can be redesigned before deployment into the production environment, or the production environment can be modified to support the new workload.

# ### Detecting Overloaded Network Servers

If the server performing a network service, such as NFS, is overloaded, it won’t be able to handle network traffic effectively. The problem could be a CPU, memory, or disk I/O bottleneck, or an inability of the server’s NIC to handle the load.

To check for a CPU bottleneck on the network server, check the CPU utilization and run queue length. GlancePlus/UX can provide this information. CPU utilization greater than 95 percent and a high processor run queue length may indicate a CPU bottleneck. One option is to increase the capacity of the server by adding more processors, but this is not always possible. Also, it may not be sufficient to fix the problem, if the service is single-threaded.

To check for a real memory bottleneck on the network server, you can first check the amount of free memory. It should not drop below 5 percent of the total available. If the system can’t keep up with the demands for memory, it will start paging and swapping. Excessive paging
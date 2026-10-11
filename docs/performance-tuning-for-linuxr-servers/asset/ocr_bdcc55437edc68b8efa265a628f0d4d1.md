# ## Benchmarks Used in This Case Study

The information collected in this case study was obtained by running the following benchmarks.

# ### NetBench

NetBench is a Ziff-Davis benchmark that measures how well a file server handles remote file I/O requests from the clients that pelt the server with requests for network file operations. NetBench reports throughput and client response time measurements. This benchmark is mainly useful for measuring the performance of the Linux TCP/IP send side (NetBench server) throughput because the receiving clients are 32-bit Windows clients for this benchmark.

# ### Netperf3

Netperf3 is a microbenchmark that tests the Linux network throughput and network scalability. Netperf3, available at http://www.netperf.org, is an experimental version. This version has multithread support and IBM enhanced Netperf3 to include multiple network interface cards (NICs) and multiclient support. These two features are added to measure the Linux network SMP and network card scalability. IBM also added another interface to test just the network drivers, bypassing the TCP/IP stack. The metric measured is throughput in megabits per second. The extended Netperf3 is available at http://www-124.ibm.com/developerworks/opensource/linuxperf/netperf/netperf3_patch.

# ### VolanoMark

VolanoMark is a Java Server benchmark that implements a chat room server to measure the performance of different implementations of Java and operating systems. Because VolanoMark is a chat room server benchmark servicing client requests, it uses the TCP/IP network for communication. Although VolanoMark also measures the performance of the scheduler and signal subsystem, the main value of this benchmark is to measure the send and receive side of the TCP/IP stack in loopback mode. The metric measured by this benchmark is messages per second.

# ### SPECWeb99

The SPECWeb99 benchmark measures a system’s capability to act as a web server servicing both static and dynamic web page requests (no SSL content). SPECWeb99 is relevant because web serving, especially with Apache, is one of the most common uses of Linux servers and their network stack. Apache is rich in functionality and is
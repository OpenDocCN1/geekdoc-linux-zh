
## Linux Kernel Component Benchmark Matrix

| Linux Kernel Component | Database Query | VolanoMark | SPECweb99 | Apache2 | NetBench | Netperf | LMBench | tiobench | IZone |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Virtual Memory | | | X | | | X | | | |
| SMP Scalability | X | X | X | X | X | X | | | |

The benchmarks discussed are selected based on a number of criteria: *industry benchmarks*, which are reliable indicators of a complex workload, and *component-level benchmarks*, which indicate specific kernel performance problems.

Industry benchmarks are generally accepted by the industry to measure the performance and scalability of a specific workload. These benchmarks often require a complex or expensive setup, which is not available to most of the OSC. However, some of these may be available to the OSC by the Open Source Development Lab (OSDL). Examples include the following:

- *SPECweb99*. Representative of web serving performance.
- *SPECsfs*. Representative of NFS performance.
- *Database query*. Representative of database query performance.
- *NetBench*. Representative of SMB file-serving performance.

Component-level benchmarks measure the performance and scalability of specific Linux kernel components that are deemed critical to a wide spectrum of workloads. Examples include the following:

- *Netperf3*. Measures the performance of the network stack, including TCP, IP, and network device drivers.
- *VolanoMark*. Measures the performance of the scheduler, signals, TCP send/receive, and loopback.
- *Block I/O test*. Measures the performance of VFS, raw and direct I/O, block device layer, SCSI layer, and low-level SCSI/fibre device driver.

Some benchmarks are commonly used by the OSC because the OSC already accepts the importance of the benchmark. Thus, it is easier to convince the OSC of performance and scalability bottlenecks illuminated by the benchmark. In addition, generally no licensing issues prevent the publication of raw data. The OSC can run these benchmarks because they are often simple to set up and the hardware required is minimal. Examples include the following:

- *Lmbench.* Used to measure performance of the Linux APIs.
- *IOzone.* Used to measure native file system throughput.
- *dbench.* Used to measure the file system component of NetBench.
- *SMB Torture.* Used to measure SMB file-serving performance.

Many benchmark options are available for specific workloads. Some important benchmarks are not listed here. For more information on specific benchmarks, see Chapter 6, "Benchmarks as an Aid to Understand Workload Performance."

## Results

It is important to understand various benchmarks, so we have chosen three benchmarks used to quantify Linux kernel performance: database query, VolanoMark, and SPECweb99. For all three benchmarks, an eight-way machine is used, as detailed in Figures 7-1 through 7-3.

**Figure 7-1. Database query benchmark results.**

![](img/08b574e80eed8279bfda286dbd25d40d_214_0.png)

Netfinity 8500R, 8-Way 700 MHz Pentium III with 2MB L2 cache, 8GB RAM, IBM ServeRAID, Red Hat 7.1, Linux kernel 2.4.6 / 2.4.16 / 2.4.17, DB2 7.1 EEE

**Figure 7-2. VolanoMark benchmark results; loopback mode.**

**Figure 7-3. SPECweb99 benchmark results using the Apache web server.**

**SPECWeb99 8-Way Performance with Apache Dynamic and Static Content**

![](img/08b574e80eed8279bfda286dbd25d40d_215_0.png)

Intel 8-Way 900 MHz Pentium III with 2MB L2 cache, 32GB RAM, (4) GB Ethernet Red Hat 7.1, Linux kernel 2.4.17, Apache 2.0.36, SPECWeb99 1.02

**VolanoMark Loopback**

![](img/08b574e80eed8279bfda286dbd25d40d_216_0.png)

UP 8P

Neftinity 8500R, 8-Way 700 Mhz Pentium III with 2MB L2 cache, 4GB RAM

Red Hat 7.1, Linux kernel 2.4.17 + patches + tuning

Figure 7-1 shows the database query benchmark results and describes the hardware and software configurations used. It also shows the progress made over a period of time in achieving the target. Some of the issues addressed have resulted in performance improvements. They include adding bounce buffer avoidance, ips, io_request_lock, readv, kiobuf, and O(1) scheduler kernel patches, as well as several DB2 optimizations.

The VolanoMark benchmark creates 10 chat rooms of 20 clients. Each room echoes the messages from one client to the other 19 clients in the room. This benchmark, not yet an open-source benchmark, consists of the VolanoChat server and a second program that simulates the clients in the chat room. It is used to measure the raw server performance and network scalability performance.

VolanoMark can be run in two modes: loopback and network. Loopback mode tests the raw server performance. Network mode tests the network scalability performance. VolanoMark uses two parameters to control the size and number of chat rooms.

The VolanoMark benchmark creates client connections in groups of 20 and measures how long it takes the server to take turns broadcasting all the clients’ messages to the group. At the end of the loopback test, it reports a score as the average number of messages transferred per second. In network mode, the metric is the number of connections between the clients and the server. The Linux kernel components stressed with this benchmark include the scheduler, signals, and TCP/IP.

Figure 7-2 shows the VolanoMark benchmark results for loopback mode. Also included is a description of the hardware and software configurations used and our target for this benchmark. We have established close collaboration with the members of the Linux kernel development team on moving forward to achieve this target. Some of the issues we have addressed that have resulted in improvements include adding the O(1) scheduler, SMP scalable timer, tunable priority preemption, and soft affinity kernel patches. As illustrated, we have exceeded our target for this benchmark; however, we are addressing some outstanding Linux kernel components and Java-related issues that we believe will further improve the performance of this benchmark.

The SPECweb99 benchmark work was conducted for research purposes only and was noncompliant. (See the "Acknowledgments" section later in this chapter for more information.) This benchmark presents a demanding workload to a web server. This workload requests 70% static pages and 30% simple dynamic pages. Sizes of the web pages range from 102 to 921,000 bytes. The dynamic content models GIF advertisement rotation. There is no SSL content. SPECweb99 is relevant because web serving, especially with Apache, is one of the most common uses of Linux servers. Apache is rich in functionality and is not designed for high performance. However, we chose Apache as the web server for this benchmark because it currently hosts more web sites than any other web server on the Internet. SPECweb99 is the accepted standard benchmark for web serving. SPECweb99 stresses the following kernel components: scheduler, TCP/IP, various threading models, sendfile, zero copy, and network drivers.

Figure 7-3 shows our results for SPECweb99. Also included is a description of the hardware and software configurations used and our benchmark target. We have a close collaboration with the Linux kernel development team and the IBM Apache team as we make progress on the performance of this benchmark. Some of the issues we have addressed that have resulted in the improvements shown include adding O(1) and read copy update (RCU) dcache kernel patches and adding a new dynamic API mod_specweb module to Apache. As shown in Figure 7-3, we have exceeded our target on this benchmark; however, we are addressing several outstanding Linux kernel component-related issues that we believe will significantly improve the performance of this benchmark.

## Summary

Linux has enjoyed great popularity, specifically with low-end and mid-range systems. In fact, Linux is regarded as a stable, highly reliable operating system to use for web servers for these machines. However, high-end, enterprise-level systems have access to gigabytes, petabytes, and exabytes of data. These systems require a different set of applications and solutions with high memory and bandwidth requirements, in addition to larger numbers of processors. This introduces a unique set of issues that may be orders of magnitude more complex than those present in smaller installations. For Linux to be competitive for the enterprise market, its performance and scalability must improve.

You should now have a sense of the strategy for improving Linux kernel performance, with special emphasis on eight-way SMP scalability. This includes an overview of several performance evaluation methodologies, including tracing, workload characterization, numerical analysis, and simulation. For benchmarking, the strategy includes understanding the hardware and software used, defining the run rules, and setting the benchmark targets. In addition, it includes measurement and analysis to find the performance issues, and proposed solutions to resolve them by creating improvements, through kernel patches to the Linux kernel, focusing on architecture-independent issues. Performance tools and benchmarks, selected to provide coverage for a diverse set of workloads and to address specific kernel components, are used to accomplish this task. Also presented are selected benchmark results, which quantify progress toward making Linux better for eight-way SMP scalability. This methodology is a means of substantiating that the performance of the Linux kernel can be improved by working with the OSC to address degradation issues. This will make Linux better and ready for the enterprise market.

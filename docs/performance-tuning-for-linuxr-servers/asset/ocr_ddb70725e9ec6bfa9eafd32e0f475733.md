| Linux Kernel Component | Database Query | VolanoMark | SPECweb99 | Apache2 | NetBench | Netperf | LMBench | tiobench | IZone |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| Virtual Memory | | | X | | | X | | | |
| SMP Scalability | X | X | X | X | X | X | | | |

The benchmarks discussed are selected based on a number of criteria: *industry benchmarks*, which are reliable indicators of a complex workload, and *component-level benchmarks*, which indicate specific kernel performance problems.

Industry benchmarks are generally accepted by the industry to measure the performance and scalability of a specific workload. These benchmarks often require a complex or expensive setup, which is not available to most of the OSC. However, some of these may be available to the OSC by the Open Source Development Lab (OSDL). Examples include the following:

+   - *SPECweb99*. Representative of web serving performance.
+   
+   - *SPECsfs*. Representative of NFS performance.
+   
+   - *Database query*. Representative of database query performance.
+   
+   - *NetBench*. Representative of SMB file-serving performance.

Component-level benchmarks measure the performance and scalability of specific Linux kernel components that are deemed critical to a wide spectrum of workloads. Examples include the following:

+   - *Netperf3*. Measures the performance of the network stack, including TCP, IP, and network device drivers.
+   
+   - *VolanoMark*. Measures the performance of the scheduler, signals, TCP send/receive, and loopback.
+   
+   - *Block I/O test*. Measures the performance of VFS, raw and direct I/O, block device layer, SCSI layer, and low-level SCSI/fibre device driver.

Some benchmarks are commonly used by the OSC because the OSC already accepts the importance of the benchmark. Thus, it is easier to convince the OSC of performance and scalability bottlenecks illuminated by the benchmark. In addition, generally no licensing issues prevent the publication of raw data. The OSC can run these benchmarks because
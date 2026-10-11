
## Table 21-2. Netperf TCP Single Stream with and Without NAPI

| Message Size (Bytes) | e1000 Baseline in Mbps | e1000 NAPI in Mbps |
| --- | --- | --- |
| 4 | 20.74 | 20.69 |
| 128 | 458.14 | 465.26 |
| 512 | 836.40 | 846.71 |
| 1024 | 936.11 | 937.93 |
| 2048 | 940.65 | 939.92 |
| 4096 | 940.86 | 937.59 |
| 8192 | 940.87 | 939.95 |
| 16384 | 940.88 | 937.61 |
| 32768 | 940.89 | 939.92 |
| 65536 | 940.90 | 939.48 |
| 131070 | 940.84 | 939.74 |

## Table 21-3. Netperf, UDP_STREAM, with and Without NAPI

| Intel e1000 Driver Baseline Throughput in Mbps | Intel e1000 Driver with NAPI Support Throughput in Mbps |
| --- | --- |
| 955.7 | 955.7 |

## Table 21-4. Packet Forwarding (Routing) with and Without NAPI

| Intel e1000 Driver Baseline Throughput in Packets Forwarded | Intel e1000 Driver with NAPI Support Throughput in Packets Forwarded |
| --- | --- |
| 305 | 298580 |

The Receive Interrupt Delay (RxIntDelay) was set to 1 in the case of NAPI because RxIntDelay=0 caused a problem, and RxIntDelay was set to 64 in the case of base e1000 driver without NAPI support. The receive and transmit descriptors were set to 256 on both systems for the e1000 driver. For the TCP Stream test, the TCP socket size was set to 131070. The test duration for both the TCP Stream and the UDP Stream was 30 seconds. One million packets at 970 kpackets per second were injected into the packet-forwarding experiments.

The packet-forwarding results in Table 21-4 clearly show that NAPI is a winner for routing packets. TCP and UDP stream tests using Netperf, as shown in Tables 21-2 and 21-3, indicate that NAPI does not improve network throughput. In fact, network throughput caused performance to moderately regress.

The results of TCP stream, UDP stream, and packet forwarding in Tables 21-2, 21-3, and 21-4 show that NAPI helped improve performance significantly in routing tests. Because NAPI is optionally available in many network drivers, you can choose to use NAPI depending on your environment.

## TCP Offload Engine Support

Server applications that do not use some of the unique features of the Linux TCP/IP protocol, such as IP filtering or quality of service (QoS), can instead use network interface cards that support TCP/IP offloading to improve network performance. TCP Offload Engine (TOE) technology consists of software extensions to existing TCP/IP stacks that enable the use of hardware planes implemented on specialized TOE network interface cards (TNICs). This hardware/software combination lets operating systems offload all TCP/IP traffic to the specialized hardware on the TNIC. As a result, the server resources are no longer needed to process TCP/IP frames and are used instead for application and other system needs, bolstering overall system performance. This sounds like a great solution for improving network performance; however, general-purpose TCP offload solutions have repeatedly failed, and TOE is suitable for some specific application environments. One of the contexts where TCP Offload is suitable is the storage-specific interconnect via commoditized network hardware, and another context is high-performance clustering solutions.

Analysis of Gigabit Ethernet workloads indicates that for every gigabit of network traffic a system processes, a GHz of CPU processing power is needed to perform the work. With the advent of higher-speed processor systems, high-performance serial PCI-Express system buses, Ethernet controllers with built-in checksum operations logic, and interrupt mitigation, users will be able to use multiple Gigabit Ethernet connections in servers without performance degradation. However, the improvement in network bandwidth also keeps pace with the improvements in other system components that necessitate a solution like TOE to improve network performance. But TCP Offload as a general-purpose solution has failed due to fundamental performance issues and the difficulties resulting in the complexities of deploying TCP Offload in practice. TOE has both proponents and opponents in the academic and commercial worlds. However, many vendors develop TNICs that are used for various workloads in addition to clustering and network storage solutions.

The TOE solutions are proprietary and vary in functionality when compared to Linux TCP/IP software stack code; unique features such IPCHAINS, IPTABLES, and general-purpose packet handling capability may not be available in these proprietary TOE solutions. Many vendors that build TNICs and drivers support different operating systems. Although our early results showed a 17% improvement in NetBench performance on Linux, the drivers used were not stable at the time they were tested, so further investigation is needed for this feature. More stable drivers and NICs should yield higher performance results.

Note that TOE is different from TCP Segmentation Offloading (TSO). TSO offloads only the segmenting of data. In the case of TSO, the TCP/IP stack hands the whole message that the application passed it to the NIC in one frame. The NIC splits the data (message) into multiple frames, building headers to each frame for transmission. This offload is done only for the send side (outbound traffic); it does not handle the inbound traffic. On the other hand, TOE offloads the whole TCP/IP stack processing to the NIC, which includes both inbound and outbound processing.

Although the TOE solution is a much-needed technology for improving network performance, how it will be adopted by the Linux open source community is yet to be seen. The contention of some in the open source community is that because the Linux TCP/IP stack already supports Zerocopy, the number of copies is already reduced. The checksum, segmentation offloading, and interrupt mitigation support in the NIC would get most of the benefit from TOE adoption, so there is no need for TOE because these remaining functions handle basic socket management and process wakeup. If the TOE solution evolves and can show a tremendous advantage over the software network stack, adoption of the TOE technology might increase.

For now, only commercial companies are developing TOE engines. As a result, the implementation of this solution varies from vendor to vendor. Perhaps the vendors will be able to mitigate or resolve the difficulties in the implementation and deployment of TOE and change the minds of skeptics who are unwilling to accept the TOE solution as a viable alternative for improving network performance.

## Case Study

This section presents the results of the benchmarks used for the case study and shows the cumulative improvements of all the performance enhancement features discussed so far. Some of the benchmarks captured the cumulative gain of all the features, whereas others captured selected gains for specific workloads.

### NetBench

Figure 21-4 summarizes the performance improvements made to the NetBench benchmark throughput through various Linux kernel and Samba enhancements and tuning. These tests were conducted on a Pentium 4 system with four 1.5GHz P4 processors, four gigabit Ethernet adapters, 2GB memory, and fourteen 15k rpm SCSI disks. SUSE version 8.0 was used for all tests. Each subsequent test included one new kernel, tuning, or Samba change. The NetBench Enterprise Disk Suite by Ziff-Davis was used for all tests.

### Figure 21-4. NetBench case study.

![](img/08b574e80eed8279bfda286dbd25d40d_579_0.png)

The following list describes the column names in Figure 21-4:

- **Baseline.** Represents a clean installation of SUSE Enterprise Linux Server 8.0 (SUSE SLES 8) with no performance configuration changes.
- **data=writeback.** A configuration change was made to the default Ext3 mount option from `ordered` to `writeback` for the /data file system (where the Samba shares reside). This improved file system performance greatly on metadata-intensive workloads such as this one.
- **smblog=1.** The Samba logging level was changed from 2 to 1 to reduce disk I/O to the Samba log files. A level of 1 is verbose enough to log critical errors.
- **SendFile/ZeroCopy.** A patch that makes Samba use SendFile for client read requests. This, combined with Linux ZeroCopy support (first available in 2.4.4), eliminates two very costly memory copies.
- **O(1) scheduler.** A small improvement that will facilitate other performance improvements in the future. The O(1) scheduler is the multiqueue scheduler that improves the performance of symmetrical multiprocessors. This is the default scheduler in the Linux 2.5 and 2.6 kernels.
- **evenly affined IRQs.** Each of the four network adapters' interrupts was handled by a unique processor. SUSE SLES 8, for P4 architecture, defaults to a round-robin assignment (destination = irq_num % num_cpus) for IRQ-to-CPU mappings. In this particular case, all of the network adapters' IRQs are routed to CPU0. This can be very good for performance because cache warmth on this code is improved, but one CPU may not be able to handle the entire network load as more NICs are added to the system. The ideal solution is to evenly affine these IRQs so that each processor handles interrupts from one NIC. Along with process affinity, this should keep the process that is assigned to a particular NIC also assigned to one CPU for maximum performance.
- **process affinity.** This technique ensures that for each network interrupt that is processed, the corresponding `smbd` process is scheduled on the same CPU to further improve cache warmth.
  > This is primarily a benchmark technique and is not commonly used elsewhere. If a workload can logically be divided evenly across many CPUs, this can be a big gain. Most workloads in practice are dynamic, and affinity cannot be predetermined.
- **/proc/sys/net/rl=763.** Increases the number of buffers held in the network stack code so that the network stack code does not have to call the memory system to get or free a buffer from and to the memory system. This tuning is not available in the 2.6 kernel.


- Case sensitivity enforced. When case sensitivity is not enforced, Samba might have to search for different versions of a filename before it can start that file, because many combinations of filenames can exist for the same file. Enforcing case sensitivity eliminates those guesses.
- Spinlocks. Samba uses fcntl() for its database, which can be costly. Using spinlocks avoids a fcntl() call. The use of the Big Kernel Lock found in posix_lock_file() reduces contention and wait times for Big Kernel Lock. To use this feature, configure Samba with --use-spin-locks, as shown in the following example:

```
Smdb --use-spin-locks -P <port_number> -0<socket option>\n-S <configuration file>
```

- Dcache read copy update. Directory entry lookup times are reduced with a new implementation of dlookup(), using the read copy update technique. Read copy update is a two-phase update method for mutual exclusion in Linux that allows avoiding of the overheads of spin-waiting locks. For more information, see the locking section of the Linux Scalability Effort project.

## Netperf3 (Gigabit Ethernet Tuning Case Study)

Gigabit Ethernet NICs are becoming cheaper and are quickly replacing 100Mb Ethernet cards. The system manufacturers are including Gigabit Ethernet on motherboards, and system suppliers and integrators are choosing Gigabit Ethernet network cards and switches for connecting disk servers, PC computer farms, and departmental backbones. This section looks at gigabit network performance in the Linux operating system and how tuning the Gigabit Ethernet improves network performance.

The Gigabit Ethernet network cards (Intel Gigabit Ethernet and Acenic Gigabit Ethernet) have a few additional features that facilitate handling high throughput. These features include support for jumbo frame (MTU) size, interrupt-delay, and TX/RX descriptors:

- Jumbo frame size. With Gigabit Ethernet NICs, the MTU size can be greater than 1500 bytes. The limitation of 1500 MTU for 100Mb Ethernet does not exist anymore. Increasing the size of the MTU usually improves the network throughput, but make sure that the network routers support the jumbo frame size. Otherwise, when the system is connected to a 100Mb Ethernet network, the Gigabit Ethernet NICs will drop to 100Mb capacity.
- Interrupt-delay/interrupt coalescence. The interrupt coalescence can be set for receive and transmit interrupts that let the NIC delay generating interrupts for the set time period. For example, when Rxint is set to 1.024us (which is the default value on Intel Gigabit Ethernet), the NIC places the received frames in memory and generates an interrupt only when 1.024us has elapsed. This can improve CPU efficiency as it reduces the context switches, but at the same time, it also has the effect of increasing receive packet latency. If properly tuned for the network traffic, interrupt coalescence can improve CPU efficiency and network throughput performance.
- Transmit and receive descriptors. This value is used by the Gigabit Ethernet driver to allocate buffers for sending and receiving data. Increasing this value allows the driver to buffer more incoming packets. Each descriptor includes a transmit and receive descriptor buffer along with a data buffer. This data buffer size depends on the MTU size; the maximum MTU size is 16110 for this driver.

Other Gigabit Ethernet studies also indicate that for every Gigabit of network traffic a system processes, approximately 1GHz of CPU processing power is needed to perform the work. Our experiment also proved that this is true, but adding more GHz processors and more Gigabit Ethernet network cards did not scale the network throughput even when the number of GHz processors equaled the number of Gigabit Ethernet NICs. Other bottlenecks, such as system buses, affect the scalability of the Gigabit Ethernet NICs on SMP processors. The NIC test shows that in only three out of four NICs media speed was achieved.

These tests were run between a Pentium 4 1.6GHz 4-way machine and four client machines (Pentium 3 1.0GHz) capable of running 1 gigabit NIC at media limit. All machines had the Linux 2.4.17 SMP vanilla kernel. The e1000 driver was version 4.1.7. These are Netperf3 PACKET_STREAM and PACKET_MAERTS runs, all with an MTU of 1500 bytes. The Pentium 4 machine had 16GB RAM with four CPUs. The four NICs were distributed equally between 100MHz and 133MHz PCI-X slots. The hyperthreading was disabled on the Pentium 4 system.

The PACKET_STREAM test transfers raw data without any TCP/IP headers. None of the packets transmitted or received go through the TCP/IP layers. This is a test that only exercises the CPU, memory, PCI bus, and the NIC's driver to look for bottlenecks in these areas. The interrupt delay and transmit and receive descriptors for the Gigabit driver were tuned with different values to determine what works best for the environment. Another element of tuning was added using different socket buffer sizes.

Table 21-5 shows that the maximum throughput achieved is 2808 Mbps out of four NICs, and the tuning that helped achieve this throughput are 4096 transmit and receive descriptors and interrupt delay set to 64 for both the receive and send sides with a 132k socket buffer size.

### Table 21-5. Intel Gigabit NICs Tuning Case Study

**Receive / Four Adapters / Four Processors / 2.4.17 Kernel**

| Descriptors, Interrupt Delay | Socket Size | Total Throughput (Mbps) | Total Dropped Packets | Driver Upper Layers | % CPU (vmstat) |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 256,16 | 131072 | 2472 | 35 | 72 | 41.0 |
| 256,16 | 65536 | 2496 | 35 | 72 | 39.2 |
| 256,16 | 32768 | 2544 | 33 | 71 | 38.2 |
| 256,64 | 131072 | 2628 | 37 | 68 | 46.6 |
| 256,64 | 65536 | 2640 | 35 | 69 | 43.2 |
| 256,64 | 32768 | 2700 | 24 | 68 | 39.6 |
| 256,96 | 131072 | 2628 | 25 | 64 | 45.2 |
| 256,96 | 65536 | 2664 | 23 | 64 | 45.6 |
| 256,96 | 32768 | 2724 | 19 | 61 | 41.2 |
| 4096,16 | 131072 | 2628 | 28 | 98 | 27.8 |
| 4096,16 | 65536 | 2664 | 29 | 98 | 28.0 |
| 4096,16 | 32768 | 2640 | 28 | 98 | 27.8 |
| 4096,64 | 131072 | 2808 | 19 | 97 | 28.6 |
| 4096,64 | 65536 | 2784 | 20 | 97 | 28.4 |
| 4096,64 | 32768 | 2664 | 25 | 97 | 30.4 |
| 4096,96 | 131072 | 2772 | 18 | 97 | 28.2 |
| 4096,96 | 65536 | 2748 | 19 | 97 | 28.6 |
| 4096,96 | 32768 | 2616 | 21 | 97 | 28.6 |

### VolanoMark

The VolanoMark benchmark creates 10 chat rooms of 20 clients. Each room echoes the messages from one client to the other 19 clients in the room. This benchmark, not yet an open source benchmark, consists of the VolanoChat server and a second program that simulates the clients in the chat room. It is used to measure the raw server performance and network scalability performance. VolanoMark can be run in two modes: loopback and network. The loopback mode tests the raw server performance, and the network mode tests the network scalability performance. VolanoMark uses two parameters to control the size and number of chat rooms.

The VolanoMark benchmark creates client connections in groups of 20 and measures how long it takes the server to take turns broadcasting all the clients’ messages to the group. At the end of the loopback test, it reports a score of the average number of messages transferred per second. In network mode, the metric is the number of connections between the clients and the server. The Linux kernel components stressed with this benchmark include TCP/IP, the scheduler, and signals.

Figure 21-5 shows the results of the VolanoMark benchmark run in loopback mode. The improvements shown resulted from various factors such as tuning the network, kernel enhancements, and two prototypo patches. The Performance team at the IBM Linux Technology Center created the prototypo patches, but they have not been submitted to the upstream kernel. The first patch is the priority preemption patch,


number of free PCI/AGP/PCI-E expansion slots. Criteria for specifying equipment to meet each of these requirements is described in more detail.

## Dual-head video cards

Although multiple single-head video cards can also be used, dual-head video cards are preferred for multi-station systems both to maximize the use of workstation expansion slots, as well as for taking advantage of the cards' on-board screen mirroring or screen spanning capabilities. In general, any recent single or dual-head video card is compatible with multi-station configurations. However, cards based on ATI's FireGL workstation or Radeon consumer chipsets, or NVIDIA's Quadro workstation or GeForce consumer chipsets are known to work and provide good driver support for multi-station configurations and other multi-monitor setups. Some video cards might work well individually but not in concert with other video cards installed in the same multi-station system. Be sure to test combinations of video cards in all anticipated multi-station configurations prior to establishing standard configurations. Figure D-1 on page 292.

> Note: Some video cards do not support 3D rendering on multiple screens simultaneously. If 3D video rendering is critical to the utility of the multi-station systems, individual models of video cards should be tested for 3D compatibility.

Useful's Desktop Multiplier system does not currently support 3D graphics acceleration software.

![](img/23b949da14ff7bab8762f0f0361af394_319_0.png)

Figure D-1 Adding a video card to an IBM IntelliStation A Pro workstation

## PCI/AGP/PCI-E expansion bus

The number of video cards (and hence, video heads) that you can install in a workstation computer is limited by the number of expansion slots on the workstation, and to a lesser extent, the bandwidth of the expansion bus. A single 32-bit PCI bus at 33 MHz is theoretically capable of transferring data at 133 Mbps, or approximately the data required to display full-screen software-decoded DVD movie streams simultaneously to six video heads with overhead (720 pixels x 480 pixels x 2 bytes/pixel x 24 frames per second x 4 video heads=99.5 Mbps). This worst case bus utilization scenario far exceeds normal workstation display usage.

In new workstations, each lane of a PCI Express expansion bus can carry up to 250 Mbps, which supports the data transfer for more than ten software decoded DVD movie streams. With up to 16 lanes for PCI Express video card, the number of available expansion slots, rather than the bandwidth, is often responsible for limiting the total number of video displays that can be connected to a multi-station system. Current IntelliStation models typically have three to five free PCI-X or PCI Express expansion slots, supporting a total of 6 to 10 single-monitor stations, or 3 to 5 dual-monitor stations per computer. In either configuration, performance of the multi-station system is not strictly limited by the bus or video cards.

When deploying high-density desktop computers to many users within the same area, PCI hardware expansion units can allow additional video cards and peripheral devices to be added to facilitate as many directly users as the systems memory, CPU, and PCI bus permit.

## Processor requirements

The optimal number of users supported by a particular CPU in a multi-station system cannot be reduced to a simple formula, because overall performance issues are largely dependent on the nature of usage. An IntelliStation system with a dual-core 2.6 GHz processor could reliably support over 20 users, simultaneously running "low utilization" applications as terminal emulators or simple data entry applications. The same system could support far fewer users, 4-8 users, with full graphical environments performing office tasks such as word processing and Web browsing. The same system used by programmers who frequently compile and test code could likely support 2 to 4 users without noticeable lag.

One method to estimate CPU usage is to examine the CPU load average, which is the number of users waiting for execution time at any given point. On a single processor system with no HyperThreading, a load average of 1.0 indicates that one process is always waiting for execution time. This is the ideal condition. A load average of more than 1.0 indicates that some processes are waiting for execution time, while a load average of less than 1.0 indicates that CPU cycles are being unused or idle.

To determine the optimal multi-station system configuration for a particular usage pattern, profile the load average for that class of users at peak usage on their current single-user systems. For best results, the load average during peak usage of all users on a multi-station system should not exceed 2.0 per processing core. A load average of 2.0 during peak usage indicates that the CPU is, in general, able to serve all regular priority user processes as required by user applications, while ignoring the usually more numerous background processes. Faster CPUs or additional processing cores can increase the computational power to decrease the amount of time it takes to service a process, and therefore increase the number of users that the system can support.

Useful's Desktop Multiplier software shares the opportunity for processor time at the X server equally for all users, but it does not attempt to modify the way in which the underlying Linux kernel handles processes and threads. Since most line-of-business applications do not spawn multi-threaded CPU-intensive processes, the combination of a dual-core processor and an SMP kernel should easily provide acceptable levels of performance for each client on the multi-station system.

As a single-station Linux desktop or thin client system, if a CPU-intensive application or event is triggered by a user on a multi-station system, all other running user processes might experience a negative performance impact from processes running in the system context Hardware-related CPU spikes arising from processes context at a higher priority than processes can negatively affect the processes of all users. Various scheduling utilities exist to set priorities for application and system-level events, as nice and renice, which are standard process management tools available with most Linux distributions. There are numerous other special schedulers available from various sources.

## Persistent storage

When considering local storage for multi-station deployments, hard disk speed and cache size tend to be more important factors than total disk size. Multi-station computers with networked file storage, the swap partition and temporary user files are unlikely to ever occupy more than 10 GB in total, but that usage would be the result of many small files. Many user applications and system processes store temporary working files in the /tmp directory. With a single user, relatively few processes read and write files to directory, and it is unlikely to grow to more than 1 GB in size with any regularity.

As a single user, responsiveness of applications as a Web browser or OpenOffice benefits from a high-performance hard disk. Applications often make and rely on many small files for each open document, which tie application responsiveness to reading and writing these small files from the hard disk quickly. On a multi-station, multi-user system, overall performance benefits greatly from a large disk cache and high spindle speed on the hard disks on which /tmp and swap files are hosted. If persistent local storage is required, local storage capacity should be provisioned according to the needs of each user, with any other desktop computer system.

## Memory

Assessing memory requirements for multi-station Linux setups is no different from assessing the memory requirements for a single user Linux workstation, with the exception that the underlying system memory image is only loaded once. Red Hat Enterprise Workstation Version 4 loads a

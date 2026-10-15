HiperSockets is customizable to accommodate varying traffic sizes. Because HiperSockets does not use an external network, it can free system and network resources, eliminating attachment costs while improving availability and performance.

# HiperSockets connectivity

HiperSockets are accessible among combinations of logical partitions (LPs) or virtual servers within the System z. This *network within the box* concept minimizes network latency and maximizes bandwidth capabilities between z/VM, Linux on System z, z/VSE, and z/OS images, or combinations of these. It is also possible to have HiperSockets under z/VM, which permits internal networks between guest operating systems, such as many Linux servers, for example.

Each HiperSockets LAN uses a Channel Path ID (CHPID) with a channel type IQD. Figure 2-11 shows an example of HiperSockets connectivity using four HiperSockets with CHPIDs FC, FD, FE, and FF.

![](bbox=[0.12, 0.54, 0.92, 0.92])
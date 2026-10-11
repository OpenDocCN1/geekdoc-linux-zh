You can use a Turbo LapLink (aka null printer) cable, which you might be able to find at a computer store, in low-speed mode (mode 0). A better solution is to create a custom cable that can support higher-speed (mode 1) transfers. To create such a cable, you need two 25-pin male connectors, a length of 25-conductor cable, and some experience in wiring custom cables. If you lack this experience, you might want to seek out somebody who possesses it. Table 18.2 shows the wiring connections for the custom cable.

| **TABLE 18.2** | High-Speed PLIP Cable Pinouts |
| --- | --- |
|  | **Computer 1** | **Computer 2** |
|  | 1 | 11 |
|  | 2 | 2 |
|  | 3 | 3 |
|  | 4 | 4 |
|  | 5 | 5 |
|  | 6 | 6 |
|  | 7 | 7 |
|  | 8 | 8 |
|  | 9 | 9 |
|  | 13 | 17 |
|  | 14 | 12 |
|  | 16 | 10 |
|  | 18 | 15 |
|  | 25 | 25 |

In Linux, parallel-port networking is referred to as Parallel Line Internet Protocol (PLIP). You must enable support for this protocol in the Linux kernel configuration, in the Network device support kernel configuration menu. After you've activated this support, you can use the parallel port as a network device with the p1p@ network device name (or possibly plp1 or plp2 if the computer has multiple parallel ports).

Because the parallel port is capable of 2MB/s speeds, PLIP is at least theoretically competitive with 10Mbps Ethernet. In practice, the parallel port is seldom as fast as Ethernet. Because Linux is the only OS to implement PLIP, this form of networking might not always be useful. You can also link only two or three computers directly in this way. You can find more information on PLIP in the /usr/src/linux/Documentation/network/PLIP.txt file and in the NET-3-4 HOWTO, which comes with all Linux distributions.
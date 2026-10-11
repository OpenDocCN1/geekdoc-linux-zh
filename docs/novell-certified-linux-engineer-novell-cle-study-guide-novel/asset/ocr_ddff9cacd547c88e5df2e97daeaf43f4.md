# CHAPTER 3 Linux Administration and Configuration

![](bbox=[0.34, 0.08, 0.86, 0.42])

**FIGURE 3.16**
PCI slots.

By default, if you have only one network board in the system, it is assigned to eth0. If you have more than one network interface in the system, the board installed in the lowest numbered PCI slot is assigned to eth0. The board installed in the next lowest-numbered PCI slot is assigned to eth1, and so on.

This seems simple on the surface. It gets tricky, however, when your motherboard uses an integrated network board.

> **TIP** An integrated network board is one that is built into the motherboard hardware itself. There is no network board installed in an expansion slot. The motherboard provides an RJ-45 jack to plug in an Ethernet cable.

If you are using only one network interface and it is the integrated interface, it will be automatically assigned to eth0. If you use the integrated interface *and* a network board installed in an expansion slot, however, either one could be assigned to eth0.

Some motherboard manufacturers build their boards such that an integrated device, such as a network board, will be assigned a lower slot number than one installed in a PCI expansion slot. I’ve encountered many systems where the built-in network adapter was assigned a very high number, whereas the first PCI expansion slot was assigned the number 1.
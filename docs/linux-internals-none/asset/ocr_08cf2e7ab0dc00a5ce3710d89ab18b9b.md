It can never be stressed enough: do not store too much data on one disk. It is tempting to use one 18GB disk instead of installing and maintaining three or four smaller disks. The professional system administrator must resist this temptation. Do we need to say why? Well, let's repeat it just for the sake of comprehensive reporting. On a disk of, say, 2GB you have x I/O that go through the whole chain as described above. On a 18GB disk, you will have 9x I/O through the same bus, same controller, and same disk device. No matter how fast the new 18GB or 31GB disks are, they will never make up for the linear increase of access compared to a small device.

# ## Character Device Handling

All devices that require the kernel to send or receive data from them one byte at a time are *character devices*. Terminals, modems, and printers all belong to this device type. On PC systems (be they workstations or servers), the primary mechanism to access devices (sound cards, SCSI controllers, graphic adapters) is *direct memory access* (DMA). The DMA is actually an area of memory within these devices mappable through RAM. This allows access to the registers of these devices, by writing to a certain RAM location. The proper handling of DMA is thus of primary importance for the kernel to be able to recognize and manage those devices attached to DMA controllers (most devices).

# ### DMA Operation

Most 64-bit platforms have special hardware that translates bus addresses (DMA addresses) to physical addresses, similar to how page tables and/or *translation lookaside buffers* (TLBs) translate virtual addresses to physical addresses. This is necessary so that PCI devices, for example, can access with a single address cycle (32-bit DMA address) any page in the 64-bit physical address space.

Previously in Linux, 64-bit platforms-such as the Alpha-had to set artificial limits on the maximum RAM size in the system, so that the `virt_to_bus()` static scheme would work (the DMA address translation tables were filled on bootup to map each bus address to the physical page `__pa`(`bus_to_virt()`).

For Linux to use dynamic DMA mapping, it needs some help from the drivers. It must take into account that DMA addresses should be
# **Preface**

header files, *time.h*, *timer.h*, *times.h*, and *timex.h* residing in the *include/linux/* directory. If a section talks about */dev/input/eventX* or */sys/devices/platform/18042/serioX/*, X is the interface number that the kernel assigns to your device in the context of your system configuration.

The [arrow image] symbol is sometimes inserted between command or kernel output to attach explanations.

Simple regular expressions are occasionally used to compactly list function prototypes. For example, the section “Direct Memory Access” in Chapter 10, “Peripheral Component Interconnect,” refers to `pci_[map|unmap|dma_sync_]single()` instead of explicitly citing `pci_map_single()`, `pci_unmap_single()`, and `pci_dma_sync_single()`.

Several chapters refer you to user-space configuration files. For example, the section that describes the boot process opens */etc/rc.sysinit*, and the chapter that discusses Bluetooth refers to */etc/bluetooth/pin*. The exact names and locations of such files might, however, vary according to the Linux distribution you use.
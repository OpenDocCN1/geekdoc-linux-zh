CFI is enabled via the kernel-configuration utility under the *Memory Technology Devices (MTD)* top-level menu. Select *Detect flash chips by Common Flash Interface (CFI)* probe under *RAM/ROM/Flash* chip drivers, as illustrated in Figure 10-3.

![](bbox=[0.07, 0.22, 0.93, 0.55])

# **FIGURE 10-3**
Kernel configuration for MTD CFI support

As shown in Listing 10-6, the Flash chip is detected via the CFI interface. Because we also enabled *CONFIG_MTD_REDBOOT_PARTS* (see Figure 10-2), MTD scans for the Redboot partition table on the Flash chip. Notice also that the chip has been enumerated with the device name *ixp4xx-Flash0*. You can see from Listing 10-6 that the Linux kernel has detected three partitions on the Flash chip, as enumerated previously using the *`fis list`* command in Redboot.

When the infrastructure is in place as described here, the Linux kernel automatically detects and creates kernel data structures representing the three Flash partitions. Evidence of these can be found in the */proc* file system when the kernel has completed initialization, as shown in Listing 10-7.
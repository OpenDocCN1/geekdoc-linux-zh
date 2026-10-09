With the utilities built, you can now install them in your target’s root filesystem:

```
```
$ make DESTDIR=$[PRJROOT]/rootfs install
```
```

This will install the utilities in `[$PRJROOT/rootfs/sbin]`. Unless your target is using udev, you will also need to create appropriate device nodes. We will see in the following sections how to create just the devices needed on the target’s root filesystem.

# How NOR and NAND Flash Work

Flash devices, including NOR flash devices such as CFI flash chips and NAND flash devices such as the DiskOnChip, are not like disk storage devices. They cannot be written to and read from arbitrarily. To understand how to operate flash chips properly, we must first look at how they operate internally. Flash devices are generally divided into *erase blocks*. Initially, an empty block will have all its bits set to 1. Writing to this block amounts to clearing bits to 0. Once all the bits in a block are cleared (set to 0), the only possible way to erase this block is to set all of its bits to 1 simultaneously. With NOR flash devices, bits can be set to 0 individually in an erase block until the entire block is full of 0s. NAND flash devices, on the other hand, have their erase blocks divided further into pages, typically of 512 bytes, which can be written only to a certain number of times—typically fewer than 10 times—before their content becomes undefined. Pages can then only be reused once the blocks they are part of are erased in their entirety. Newer NAND flash chips known as MLC or Multi Level Cell flash reduce the number of writes per page to only one.

# Native CFI Flash

Most recent small- to medium-size non-x86 embedded Linux systems are equipped with some form of CFI flash. Setting up CFI flash to be used with Linux is relatively easy. In this section, we will discuss the setup and manipulation of CFI devices in Linux. We will not discuss the use of filesystems on such devices, however, since these will be covered in the next chapter. The order of the subsections follows the actual steps involved in using CFI flash devices with Linux as much as possible. You can, nevertheless, use these instructions selectively according to your current manipulation.

# Kernel configuration

You will need to enable kernel support for the following options to use your CFI flash device:

+   • MTD support
+   • MTD partitioning support if you would like to partition your flash device
+   • Direct char device access to MTD devices
+   • Caching block device access to MTD devices
+   • In the “RAM/ROM/Flash chip drivers” submenu, detect flash chips by CFI probe
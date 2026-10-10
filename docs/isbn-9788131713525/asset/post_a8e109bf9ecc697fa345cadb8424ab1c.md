
## 10.3.4 Flash Chip Drivers

MTD has support for a wide variety of Flash chips and devices. Chances are very good that your chosen chip has also been supported. The most common Flash chips support the Common Flash Interface (CFI) mentioned earlier. Older Flash chips might have JEDEC support, which is an older Flash compatibility standard. Figure 10-4 shows the kernel configuration from a recent Linux kernel snapshot. This version supports many Flash types.

![](img/7a1144833e62564667e7dd9eb4c9f03d_294_0.png)

### FIGURE 10-4
Flash device support

If your Flash chip is not supported, you must provide a device file yourself. Using one of the many examples in `../drivers/mtd/chips` as a starting point, customize or create your own Flash device driver. Better yet, unless the chip was just introduced with some ransfigled interface, chances are good that someone has already produced a driver.

## 10.3.5 Board-Specific Initialization

Along with a mapping driver, your board-specific (platform) setup must provide the underlying definitions for proper MTD Flash system operation. Listing 10-12 reproduces the relevant portions of `../arch/arm/mach-1px4xxx/coyote-setup.c`.

### Listing 10-12
**Coyote-Specific Board Setup**

```
static struct flash_platform_data coyote_flash_data = {
  .map_name = "cfi_probe",
  .width = 2,
};

static struct resource coyote_flash_resource = {
  .start = COYOTE_FLASH_BASE,
  .end = COYOTE_FLASH_BASE + COYOTE_FLASH_SIZE - 1,
  .flags = IORESOURCE_MEM,
};

static struct platform_device coyote_flash = {
  .name = "IXP42X-Flash",
  .id = 0,
  .dev = {
    .platform_data = &coyote_flash_data,
  },
  .num_resources = 1,
  .resource = &coyote_flash_resource,
};
...

static struct platform_device *coyote_devices[] __initdata = {
  &coyote_flash,
  &coyote_uart
};

static void __init coyote_init(void)
{
  ...
  platform_add_devices(coyote_devices,
                       ARRAY_SIZE(coyote_devices));
}
...
```

In Listing 10-12, only the relevant portions of the coyote-setup.c platform initialization file are reproduced. Starting from the bottom, the coyote_init() function calls platform_add_devices(), specifying the Coyote-specific devices defined earlier in this file. You'll notice that two devices are defined just above the coyote_init() routine. The one we're interested in for this discussion is coyote_flash. This structure of type struct platform_device contains all the important details needed by the Linux kernel and MTD subsystem.

The `.name` member of the `coyote_flash` structure binds our platform-specific Flash resource to a mapping driver with the same name. You can see this in the mapping driver file `.../drivers/mtd/maps/ixp4xx.c`. The `.resource` member communicates the base address of the Flash on the board. The `.dev` member, which contains a `.platform_data` member, ties our Flash setup to a chip driver. In this case, we have specified that our board will use the CFI probe method, specified in the kernel configuration as `CONFIG_MTD_CFI`. You can see this configuration selection in Figure 10-4.

Depending on your own architecture and board, you can use a method similar to this to define the Flash support for your own board.

## 10.4 MTD Utilities

The MTD package contains a number of system utilities useful for setting up and managing your MTD subsystem. The utilities are built separately from the primary MTD subsystem, which should be built from within your Linux kernel source tree. The utilities can be built in a similar manner to any other cross-compiled user space code.

You must use caution when using these utilities because there is no protection from mistakes. A single-digit typo can wipe out the bootloader on your hardware platform, which can definitely ruin your day unless you've backed it up and know how to reprogram it using a JTAG Flash programmer.

In keeping with a common practice throughout this book, we cannot devote sufficient space to cover every MTD utility. We highlight the most common and useful ones, and leave it as an exercise for the reader to explore the rest. A recent MTD snapshot contained more than 20 binary utilities.

The `flash_*` family of utilities is useful for raw device operations on an MTD partition. These include `flashcp`, `flash_erase`, `flash_info`, `flash_lock`, `flash_unlock`, and others. Hopefully their names are descriptive enough to give you some idea of their function. After partitions are defined and enumerated as kernel devices, any of these user space utilities can be run on a partition. We repeat the warning we issued earlier: If you execute `flash_erase` on the partition containing your bootloader, you'll be the proud owner of a silicon paperweight. If you intend to experiment like this, it’s a good idea to have a backup of your bootloader image and know how to re-Flash it using a hardware JTAG emulator or other Flash programming tool.

Our new partition created in Listing 10-8 (*MyKernel*) shows up in the kernel running on the Coyote board, as detailed in Listing 10-13. Here you can see the new partition we created instantiated as the kernel device `mtd1`.

### Listing 10-13
**Kernel MTD Partition List**

```
root@coyote:~# cat /proc/mtd
dev:    size erasesize name
mtd0: 00060000 00020000 "RedBoot"
mtd1: 00160000 00020000 "MyKernel"  
mtd2: 00001000 00020000 "RedBoot config"
mtd3: 00020000 00020000 "FIS directory"
```

Using the MTD utilities, we can perform a number of operations on the newly created partition. The following shows the results of a `flash_erase` command on the partition:

```
$ flash_erase /dev/mtd1
Erase Total 1 Units
Performing Flash Erase of length 131072 at offset 0x0 done
```

To copy a new kernel image to this partition, use the `flashcp` command:

```
root@coyote:~# flashcp /workspace/coyote-40-zImage /dev/mtd1
```

It gets a bit more interesting working with a root file system partition. We have the option of using the bootloader or the Linux kernel to place the initial image on the Redboot flash partition. First, we use Redboot to create the new partition that will hold our root file system. The following command creates a new partition on the Flash called `RootFS` starting at physical memory 0x50300000, with a length of 30 blocks. Remember, a block, generically called an erase unit, is 128KB on this Flash chip.

```
RedBoot> fis create -f 0x50300000 -l 0x5060000 -n RootFS
```

Next, we boot the kernel and copy the root file system image into the new partition we have named `RootFS`. This is accomplished with the following command from a Linux command prompt on your target board. Note that this assumes you have already placed your file system image in a directory accessible to your board.

As mentioned many times throughout this book, NFS is your best choice for development.

```
root@coyote:-# flashcp /roothfs.ext2 /dev/mtd2
```

The file system can be anywhere from a couple megabytes up to the largest size we have allowed on this partition, so this can take some time. Remember, this operation involves programming (sometimes called “flashing”) the image into the Flash memory. After copying, we can mount the partition as a file system. Listing 10-14 displays the sequence.

### Listing 10-14
**Mounting MTD Flash Partition as ext2 File System**

```
root@coyote:-# mount -t ext2 /dev/mtdblock2 /mnt/remote ro
root@coyote:-# ls -l /mnt/remote

    total 16
drwxr-xr-x    2 root     root          1024 Nov 19  2005 bin
drwxr-xr-x    2 root     root          1024 Nov 26  2005 boot
drwxr-xr-x    2 root     root          1024 Nov 19  2005 dev
drwxr-xr-x    5 root     root          1024 Nov 19  2005 etc
drwxr-xr-x    2 root     root          1024 Oct 26  2005 home
drwxr-xr-x    3 root     root          1024 Nov 19  2005 lib
drwxr-xr-x    3 root     root          1024 Nov 19  2005 mnt
drwxr-xr-x    2 root     root          1024 Oct 26  2005 opt
drwxr-xr-x    2 root     root          1024 Oct 26  2005 proc
drwxr-xr-x    2 root     root          1024 Nov 19  2005 sbin
drwxr-xr-x    2 root     root          1024 Oct 26  2005 srv
drwxr-xr-x    2 root     root          1024 Oct 26  2005 sys
drwxr-xr-x    2 root     root          1024 Oct 26  2005 tmp
drwxr-xr-x    6 root     root          1024 Nov 19  2005 usr
drwxr-xr-x    2 root     root          1024 Nov 19  2005 var
root@coyote:-#
```

Listing 10-14 has two important subtleties. Notice that we have specified /dev/mtdblock2 on the mount command line. This is the MTD block driver that enables us to access the MTD partition as a block device. Using /dev/mtd2 as a specifier instructs the kernel to use the MTD character device. Both the mtdchar and mtdblock are pseudodevices used to provide either character-based or block-oriented access to the underlying Flash partition. Because mount expects a block device, you must use the block-device specifier. Figure 10-1 shows the kernel configuration that enables these access methods. The respective kernel configuration macros are CONFIG_MTD_CHAR and CONFIG_MTD_BLOCK.

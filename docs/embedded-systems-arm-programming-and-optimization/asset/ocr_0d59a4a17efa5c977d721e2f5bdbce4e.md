# A.4 Installing the Kernel 235

# A.3 BUILDING THE KERNEL

On your workstation, define the $CCPREFIX environment variable to:

```
<tools directory root~/arm-bcm2708/arm-bcm2708-linux-gnueabi/
bin/arm-bcm2708-linux-gnueabi-n
```

Next, define the KERNEL_SRC environment variable to the root of your kernel source code.

Copy and decompress your Raspberry Pi’s current kernel build to the kernel source directory with the filename “.config”. The kernel configuration is stored in the compressed file /proc/config.gz on the Raspberry Pi.

You can use the “zcat” command to perform the decompression, that is,

```
zcat config.gz > $KERNEL_SRC/.config
```

Change to the root of the kernel source and issue the following command, which will ensure that the .config file is correct. Due to minor differences between your current kernel and the downloaded kernel, this command may prompt you for a few build options. If so, just push enter to accept the default responses.

```
make ARCH=arm CROSS_COMPILE=$CCPREFIX oldconfig
```

Use the following command to build the kernel. This step may take a significant amount of time.

```
make ARCH=arm CROSS_COMPILE=$CCPREFIX
```

Use the following command to build the modules.

```
make ARCH=arm CROSS_COMPILE=$CCPREFIX modules
```

Finally, on the Raspberry Pi itself, issue the following command in Linux kernel source root. This will install the modules.

```
make modules_install
```

# A.4 INSTALLING THE KERNEL

The new kernel image will be located in the kernel source at /arm/boot/zImage. Copy this file to /boot/kernel.img and reboot.

After the reboot, re-check the /sys/bus/event_source/devices directory for perf_event support.
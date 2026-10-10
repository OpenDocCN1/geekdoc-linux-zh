Thus starts the long and sometimes frustrating learning curve of embedded Linux! Many things that can go wrong could lead to this common failure. With some knowledge and a JTAG debugger, there are ways to determine what went awry.

# 14.5.1 Early Serial Debug Output

The first tool you might have available is CONFIG_SERIAL_TEXT_DEBUG. This Linux kernel-configuration option adds support for debug messages very early in the boot process. At the present time, this feature is limited to the PowerPC architecture, but nothing prevents you from duplicating the functionality in other architectures. Listing 14-22 provides an example of this feature in use on a PowerPC target using the U-Boot bootloader.

# **Listing 14-22**
**Early Serial Text Debug**

```
#! Booting image at 00200000 ...
Image Name: Linux-2.6.14
Created: 2005-12-19 22:24:03 UTC
Image Type: PowerPC Linux Kernel Image (gzip compressed)
Data Size: 607149 Bytes = 592.9 kB
Load Address: 00000000
Entry Point: 00000000
Verifying Checksum ... OK
Uncompressing Kernel Image ... OK
#mach(): Done <- = Start of messages enabled by
#hw:enter <- = CONFIG_SERIAL_TEXT_DEBUG
#hw:hwinit
#hw:mapin
#hw:setio
#hw:exit
setup_arch: enter
setup_arch: bootmem
arch: exit
arch: real exit
```

Using this feature, you can often tell where your board is getting stuck during the boot process. Of course, you can add your own early debug messages in other places in the kernel. Here is an example of its usage found in .../arch/ppc/mm/init.c:

```
/** Map in all of RAM starting at KERNELBASE **/
if (ppc_md.progress)
ppc_md.progress("#hw:mapin", 0x301);
mapin_ram();
```
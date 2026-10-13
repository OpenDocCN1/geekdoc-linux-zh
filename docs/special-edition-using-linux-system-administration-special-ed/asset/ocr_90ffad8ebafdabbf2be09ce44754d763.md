can be specified by command line options to LILO. The initrd= lines specify the RAM disk images that are available if you need to boot an alternate root file system in a RAM disk for system maintenance purposes. These kernel image names and locations are stored in the LILO map file.

The prompt option instructs the boot loader to always prompt for command-line options that can be entered at boot time. The timeout=50 option sets a timeout of five seconds for the prompt. If no command-line options are entered, the system will continue booting after waiting for five seconds.

The delay=100 instructs the boot loader to wait ten seconds if the Shift key is pressed during booting. Otherwise the first kernel image mentioned is booted. If the Shift key is pressed, the boot loader prompts for the name of the kernel image to boot. This option is very useful when you install a new kernel. LILO provides a method to boot the older kernel, just in case there are problems with the new one.

Many possibilities and options are available with LILO. To learn about LILO, read the documentation—Technical_Guide.ps and User_Guide.ps typically found in the directory `/usr/doc/lilo-0.21`.

# KERNEL INITIALIZATION AND HARDWARE CONFIGURATION

In this phase of booting the kernel has been loaded by LILO and starts executing and initializing itself. One of the first things the kernel does is to check the available memory on the system. The kernel reserves a fixed amount of memory for itself, its internal data stores, and buffers. A message to this effect is printed on the system console and also recorded in `/var/log/dmesg`. For example, a message such as the following is printed about the available system memory and how much of it is reserved by the kernel.

```
Memory: 387200k/393216k available (1044k kernel code, 416k reserved,\
  4184k data, 68k init)
```

After the kernel has initialized itself it starts probing the system to see what devices are present. When a custom kernel is built it is usually configured to include a set of drivers for devices that are expected to be on the system. A generic kernel can contain support for many more devices than you actually have on your system. As the kernel detects these devices it prints very brief messages about them. The following is sample output of boot up messages on a dual CPU machine that shows the various devices the kernel has detected and configured. The output messages on your system will vary depending on the type of hardware and peripherals installed:

```
Linux version 2.2.5-15smp (root@porky.devel.redhat.com) (gcc version egcs-2.91.66
 19990314/Linux (egcs-1.1.2 release)) #1 SMP Mon Apr 19 22:43:28 EDT 1999
Intel MultiProcessor Specification v1.4
        Virtual Wire compatibility mode.
OEM ID: COMPAQ Product ID: PROLIANT  APIC at: 0xFEE00000
Processor #1 Pentium(tm) Pro APIC version 16
Processor #0 Pentium(tm) Pro APIC version 16
```
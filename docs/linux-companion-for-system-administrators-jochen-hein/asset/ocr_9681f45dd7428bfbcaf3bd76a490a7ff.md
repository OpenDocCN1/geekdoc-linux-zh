# 3.3.1 Kernel parameters

Many initializations (for example I/O addresses for expansion boards) of the kernel can be influenced by means of command line parameters. These parameters are passed to the kernel by the boot loader.

debug

Sets console_loglevel to 10, activating 'verbose' console messages.

mem=size

Sets the size of the physical memory. This may be necessary when the RAM size cannot be determined automatically, for example in computers with more than 64 Mbytes of RAM.

no387

The above maths coprocessor is not used.

no-hlt

Prevents use or execution of the HLT instruction of more recent Intel (-compatible) processors when the system is idle. When this instruction is used, the CPU is less heated and laptops consume significantly less power, but some machines may hang.

reserve=port1,num1,[portn,numn]

Excludes I/O ports and zones from auto-probing. This is needed, for example, when auto-probing leads to 'hanging' of the system. port1 represents the first address, num1 indicates the number of addresses to be excluded from port1 onward. You may repeat portn, numn until you have all parts excluded that you wanted to exclude.

root=device

Changes the device used as root file system. This overwrites the specifications stored in the kernel image. device is either a device name such as /dev/hda3 or a hexadecimal device number.

ro or rw

The root partition is mounted into the directory tree read-only or/write.
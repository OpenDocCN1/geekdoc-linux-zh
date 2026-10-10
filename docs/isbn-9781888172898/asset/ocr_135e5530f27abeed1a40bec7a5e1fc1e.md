# D.5.6  Loading MILO from the SRM Console

The SRM (short for System Reference Manual) Console knows nothing about file systems or disk-partitions, it simply expects that the secondary bootstrap loader occupies a consecutive range of physical disk sectors starting from a given offset. The information describing the secondary bootstrap loader (its size and offset) is given in the first 512 byte block. To load MILO via the SRM you must generate that structure on a device which the SRM can access (such as a floppy disk). This is what mboot and bootm, mboot is the first block (or boot description) and mboot is the MILO image rounded up to a 512 byte boundary.

To load MILO from a boot block device, either build mboot and bootm and push them onto the boot device using the following command:

```
```text
$ cat mboot bootm > /dev/fd0
```
```

Or, grab the appropriate MILO. dd from a web site and write it onto the boot device using either RAWRITE.EXE or dd.

Once you have done that you can boot the SRM console and use one of its many commands to boot MILO. For example, to boot MILO from a boot block floppy you would use the following command:

```
```text
>>boot dva0
(boot dva0 0.0.0.1 -flags 0)
block 0 of dva0.0.0.0.1 is a valid boot block
reading 621 blocks from dva0.0.0.0.1
bootstrap code read in
base = 112000, image_start = 0, image_bytes = 4da00
initializing HWRB at 2000
initializing page table at 104000
initializing machine state
setting affinity to the primary CPU
jumping to bootstrap code
MILO Stub: V1.1
Unzipping MILO into position
Allocating memory for unzip
####...
```
```

The following systems are *known* to have SRM Console support:
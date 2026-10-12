+   ● Noname (Section E.5.6)
+   ● EB66+ (Section E.5.6)
+   ● EB164 (Section E.5.6)

# E.5.5 Loading Milo from the SRM Console

The SRM (short for System Reference Manual) Console knows nothing about filesystems or disk-partitions, it simply expects that the secondary bootstraps loader occupies a consecutive range of physical disk sectors starting from a given offset. The information describing the secondary bootstrap loader (its size and offset) is given in the first 512 byte block. To load Milo via the SRM you must generate that structure on a device which the SRM can access (such as a floppy disk). This is what mboot and boom, mboot is the first block (or boot description) and boom is the Milo image rounded up to a 512 byte boundary.

To load Milo from a boot block device, either build mboot and boom and push them onto the boot device using the following command:

```
$ cat mboot boom > /dev/fd0
```

Or, grab the appropriate milo.dd from a web site and write it onto the boot device using either RAWRITE.EXE or dd.

Once you have done that you can boot the SRM console and use one of its many commands to boot Milo. For example, to boot Milo from a boot block floppy you would use the following command:

```
>>boot dva0
(boot dva0.0.0.0.1 -flags 0)
block 0 of dva0.0.0.0.1 is a valid boot block
reading 621 blocks from dva0.0.0.0.1
bootstrap code read in
base = 112000, image_start = 0, image_bytes = 4da00
initializing HWRPB at 2000
initializing page table at 104000
initializing machine state
setting affinity to the primary CPU
jumping to bootstrap code
```
# INSTALLATION

problems do occur (for example, with very large hard disks), this section will provide you with a better understanding of the terminology of warnings and error messages.

In theory, Linux supports partitions of up to 4 Tbytes (terabytes, that is, 1024 GBytes). In practice, you will not be able to exploit this to its full extent, as for the time being there are no hard disks that are big. But, depending on your hardware, you must be prepared to run into difficulties with disks as small as 504 Mbytes. The origin of the problem lies in the very far-sighted BIOS design. Once Linux is up and running, it is independent of the BIOS and can address the entire hard disk.

In order to understand the problem better, we need some background information. The size of hard disk is determined by three parameters: cylinders, heads, and sectors. This triplet of numbers is commonly called the CHS geometry of the hard disk (cylinder, head, sector); sometimes you will find the term 3D address (LILO documentation) – it means the same.

For historical reasons, there are various limits for CHS values: the BIOS allows a maximum of 1024 cylinders, 256 heads, and 63 sectors. IDE disks, in turn, provide a maximum of 65536 cylinders, 16 heads, and 255 sectors. The smaller the thus lead to the logical limit of 504 Mbytes (1024 cylinders, 16 heads, 63 sectors, 512 bytes per sector).

> CHS values have not related to the physical disposition of a hard disk for a long time. The hard disk has a predetermined CHS triple and behaves as it really does have many cylinders, heads, and sectors. In reality, the construction of the disk and the disposition of data look totally different – but this is the responsibility of the hard disk electronics.

# BIOS arithmetic

The way out of this dilemma is usually an adapted BIOS version, as is common nowadays with all SCSI and EIDE controllers. The BIOS is still not allowed to signal more than 1024 cylinders (that would not be compatible with DOS/Windows 3.1/Windows 95), but it can manipulate the remaining values: a disk which pretends to have 2100 cylinders and 16 heads (physical CHS value) seemingly becomes one with 525 cylinders and 64 heads (logical CHS value, often called XCHS).

You can find out that geometry is valid under DOS by calling the program DPARAM.COM. This program is started under DOS with the parameter 0x80 (for the first disk) or 0x81 (for the second disk) and yields the number of cylinders, heads, and sectors. You will find the program on Linux CDs (usually in itsits directory).

The theoretical maximum (still DOS compatible) is now 7.9 Gbytes (1024 cylinders, 256 heads, 63 sectors), which is nowadays too small. When this book reaches the shelves, there will be EIDE hard disks of up to 25 Gbytes around – maybe even larger.)
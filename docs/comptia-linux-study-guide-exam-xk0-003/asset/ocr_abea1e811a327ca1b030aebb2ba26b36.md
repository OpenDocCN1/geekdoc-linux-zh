GPT employs three data structures, two of which have backups:

**Protective MBR** An MBR exists on a GPT-partitioned disk, with the purpose of deterring creation of ordinary MBR partitions. The protective MBR, as it’s called, defines a single partition with a type code of 0xEE (EFI GPT). This partition spans the size of the disk or 2TB, whichever is smaller, thus signalling that the disk is a GPT disk and (in **is hoped**) minimising accidental damage should a GPT unaware utility be used to access the disk. The protective MBR may also hold a boot loader in its code area.

**Header** The header defines various GPT metadata, such as the size of the partition table, the locations of the partition tables, and cyclic redundancy check (CRC) checksums to help system software detect data corruption.

**Partition table** The partition table defines actual partitions. On most disks, the partition table can define up to 128 partitions. GPT does away with the primary/extended/logical distinction of MBR, which simplifies certain disk administration tasks. In Linux, GPT partitions are numbered starting with 1, and they need not be consecutive, so you could have partitions numbered 2, 5, 23, and 120. (Many disk utilities will automatically change such a sequence to 1, 2, 3, and 4, however.)

The GPT header and partition table are duplicated: one copy appears at the start of the disk, and the other copy appears at the end of the disk. This redundancy, along with the CRCs in the header, simplifies some types of data recovery.

GPT’s main drawback is that support for it is relatively immature. The *fdisk* utility (described shortly in “Partitioning Tools”) doesn’t work with GPT disks. The old LILO boot loader and some versions of GRUB also don’t support it. GPT support must also be enabled in your kernel. (Most distributions do so by default.) The situation is worse in some OSs—particularly older ones. Nonetheless, you should be at least somewhat familiar with GPT because of MBR’s inability to handle disks larger than 2TB.

# Linux Partition Requirements

To Linux, there’s very little difference between the primary and logical partitions or even between MBR and GPT partitions. As noted earlier, there are numbering implications for the different partitioning schemes, and you should be familiar with them.

Some administrators use a primary Linux boot partition because a conventional x86 boot loader can boot only from a primary partition. When the computer does so, it runs code in the boot sector of the boot partition. Typically, Linux places a special boot loader program in this location. The *Grand Unified Boot Loader (GRUB)* and the *Linux Loader (LILO)* are the two boot loaders most commonly found on x86 Linux systems. Alternatively, GRUB or LILO can reside directly in the MBR, which is more direct but leaves the boot loader more vulnerable to being wiped out should some other utility rewrite the MBR. Placing GRUB in the protective MBR is the only option if you’re booting a BIOS-based system from a GPT disk.
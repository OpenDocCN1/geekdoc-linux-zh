exclamation point, such as `!51e67cb5-6ecf-11d6-8ff8-00022d09712b`. These partition types are common across all operating system, but most OSs provide human-friendly names for these human-hostile GUIDs. This book uses the human-friendly names; check `gpart(8)` for the human-hostile ones.

The most common partition types you'll see on a FreeBSD system include the following:

+   - **freebsd-boot** FreeBSD boot loader
+   - **freebsd-ufs** FreeBSD UFS filesystem
+   - **freebsd-zfs** FreeBSD ZFS filesystem
+   - **freebsd-swap** FreeBSD swap partition
+   - **efi** An EFI system partition, used to boot from EFI

You might also see these GPT partition types. Don't use them in modern FreeBSD, but know that their presence might help you identify just what that weird disk is and how to crack it open.

+   - **freebsd** A GPT partition that's divided into `bsdlablel(8)` partitions
+   - **freebsd-vinum** A partition controlled by `gvinum(8)`
+   - **mbr** A partition subdivided into MBR partitions
+   - **ntfs** A partition containing a Microsoft NTFS filesystem
+   - **fat16, fat32** Partitions containing FAT

For a complete listing of recognized partition types, see `gpart(8)`.

# Creating GPT Partitions

Partitioning disks is easy: figure out which partitions you want, create them, and go. The tricky part is living with your partitioning. Before creating partitions, decide what you're going to do with this disk. How much space do you have? How do you want to divide it? Before you start creating partitions, write down exactly what you want to achieve.

Here, I'm manually partitioning a 1TB disk for a UFS FreeBSD install. It'll need a 512KB boot partition (type `freebsd-boot`) and 8GB for
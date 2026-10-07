floppy disks; 16-bit FATs allow partitions of up to 2GB; and 32-bit FATs support partitions of up to 2TB. Linux's FAT drivers auto-detect the FAT size, which is often indicated as a suffix to the filesystem name, as in FAT–16 and *EXFAT–32*.

+   - Filename length: The original FAT filesystem, as used by DOS, supported only eight-character filenames with an optional three-character extension (the so-called 8.3 filename limit). With Windows 95, Microsoft introduced an extension to FAT known as VFAT, which supports long filenames. Linux supports its own FAT extension, known as UMDSDOS, which places Linux ownership and permissions information on FAT filesystems along with long filenames. VFAT and UMDSDOS are incompatible extensions.

Because Linux auto-detects the FAT size, there's no need to use separate Linux filesystem types for different FAT sizes. Linux uses three type codes for each of the filename length options, however. If you mount a filesystem with the msdos type code, Linux restricts filenames to 8.3 limits. If you use the vfat type code, Linux uses VFAT long filenames. If you use umsdos, Linux uses UMDSDOS long filenames. In most cases, vfat is the most appropriate type code with which to access FAT partitions, because it allows for exchange of files with long filenames between Linux and Windows systems.

**Note** A common misconception is that FAT–32 and VFAT are somehow linked. They aren't. You can access a FAT–16 or even FAT–12 disk using VFAT long filenames; and you can mount a FAT–32 partition with the Linux msdos driver to use only 8.3 filenames.

UMSDOS is unusual because it allows Linux to treat a FAT partition like a native filesystem. You can run a Linux system entirely from a UMDSDOS partition, and in fact some distributions support installing Linux directly on a UMDSDOS partition. This configuration tends to be slow, however, because Linux's FAT support, although stable, isn't as fast as its support for ext2fs.

# Apple Filesystems

If you run Linux on a Macintosh or need to exchange data with Macintosh users, you're likely to need support for a Macintosh filesystem. In 2002, four such filesystems exist, although only three are in common use and only two support Linux drivers:

**MFS** The *Macintosh Filesystem (MFS)* was used by the earliest Macintoshes. It's almost never used on anything but 400KB floppy disks, which are extremely rare today. Linux does not include MFS support.

**HFS** The *Hierarchical Filesystem (HFS)* was the replacement for MFS. Used on 800KB and larger floppy disks and all Macintosh hard disks until 1998, HFS is quite common in the Macintosh world. The Linux 2.2.x and later kernels include read/write HFS support, using the filesystem type code hfs. The write support is considered experimental, however, and occasionally damages hard disks. It's therefore best to restrict use of this support to blank floppy disks. Macintosh CD-ROMs often use HFS rather than ISO–9660.

**Note** Although 800KB Macintosh floppies use HFS, Linux cannot read these disks, even with an HFS-enabled kernel. These disks use an uncommon low-level disk-recording technique, and standard x86 hardware cannot cope with it. Apple switched to PC–style low–level recording technologies with its 1.44MB floppies, so Linux can read Macintosh 1.44MB floppies, as well as other removable media.

138
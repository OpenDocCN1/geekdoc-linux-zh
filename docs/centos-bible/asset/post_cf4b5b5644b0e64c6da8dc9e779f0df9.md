
# Part III

## Administration

not be in use at the moment, or they may not be built into your current kernel (so they may need to be loaded as modules).

- **adfs** — This is the acorn disc file system, which is the standard file system used on RiscOS operating systems.
- **befs** — This is the file system used by the BeOS operating system.
- **cifs** — The Common Internet File System (CIFS) is the virtual file system used to access servers that comply with the SNIA CIFS specification. CIFS is an attempt to refine and standardize the SMB protocol used by Samba and Windows file sharing.
- **ext3** — The ext file systems are the most common file systems used with Linux. The ext3 file system is currently the default file system type in many Linux systems (including CentOS). The root file system (`/`) is typically ext3 (although you can use other file systems as well). The ext3 file system is also referred to as the Third Extended file system. The ext3 file system includes journaling features that improve a file system’s ability to recover from crashes, as compared to ext2 file systems.
- **ext4** — An enhancement to ext3, this type of file system performs and scales better to larger numbers of files, but ext4 is still considered experimental.
- **ext2** — The default file system type for versions of older CentOS releases. Features are the same as ext3, except that ext2 doesn’t include journaling features.
- **ext** — This is the first version of the ext file system. It is not used very often anymore, and I recommend that you don’t use it.
- **iso9660** — This file system evolved from the High Sierra file system (which was the original standard used on CD-ROM). Extensions to the High Sierra standard (called *Rock Ridge extensions*), allow iso9660 file systems to support long filenames and UNIX-style information (such as file permissions, ownership, and links). This file system type is used when you mount a CD-ROM.
- **kafs** — This is the AFS client file system. It is used in distributed computing environments to share files with Linux, Windows, and Macintosh clients.
- **minix** — This is the Minix file system type, used originally with the Minix version of UNIX. It only supports filenames of up to 30 characters.
- **msdos** — This is an MS-DOS file system. You can use this type to mount floppy disks that come from Microsoft operating systems.
- **vfat** — This is the Microsoft extended FAT (VFAT) file system.
- **umsdos** — This is an MS-DOS file system with extensions to allow features that are similar to UNIX (including long filenames).
- **proc** — This is not a real file system, but rather a file-system interface to the Linux kernel. You probably won’t do anything special to set up a proc file system. However, the `/proc` mount point should be a proc file system. Many utilities rely on `/proc` to gain access to Linux kernel information.
- **swap** — This is used for swap partitions. Swap areas are used to hold data temporarily when RAM is currently used up. Data is swapped to the swap area, then returned to RAM when it is needed again.
- **nfs** — This is the Network File System (NFS) type of file system. File systems mounted from another computer on your network are this type of file system.

![](img/2f265415ceec72538dd3c78ffca75c10_404_0.png)

> Information on using NFS to export and share file systems over a network is contained in Chapter 17.

- **hpfs** — This file system is used to do Read Only mounts of an OS/2 HPFS file system.
- **ncpfs** — This relates to Novell NetWare file systems. NetWare file systems can be mounted over a network.
- **ntfs** — Many people who set up dual-boot computers want to be able to access the Windows (ntfs) drives. To add NTFS file system support to CentOS, you need to install the fuse and fuse-ntfs-3g packages available from the RPMForge repository.
- **affs** — This file system is used with Amiga computers.
- **reiserfs** — This is a journaling file system that used to be the default file system for some other Linux distributions (including SUSE, Slackware, and Linspire). Reiserfs is not considered to be well-supported in CentOS systems.
- **ufs** — This file system is popular on Sun Microsystems operating systems (i.e., Solaris and SunOS).
- **xenix** — This was added to be compatible with Xenix file systems (one of the first PC versions of UNIX). The system is obsolete and will probably be removed eventually.
- **xfs** — This is a journaling file system that is useful in high-performance environments. It includes full 64-bit addressing. An xfs file system can scale up to systems that include multiple terabytes of data that transfer data at multiple gigabytes per second. The CentOSPlus repository contains the `kmod-xfs` and `xfsprogs` RPMs you need to implement xfs easily on CentOS.
- **jfs** — This file system is based on the JFS file system IBM used for OS/2 Warp. It became an Open Source project in 2000. JFS is most suited for enterprise systems. Like XFS, JFS is tuned for large file systems and high-performance environments.
- **xiafs** — This file system supports long filenames and larger inodes than file systems such as minix.
- **squashfs** — This is a compressed file system, where files are uncompressed on the fly as they are requested. It is often used with live CDs.
- **fuse** — Fuse behaves like a user-space remote file system. A local user can use ssh tools to mount a remote file system locally, without the remote file system being made available, purely on the basis of the permissions of the user you log in as. A very cool way to mount a remote file system without administrative intervention on the remote side!

The ext4 file system is the latest version of the ext file system (with ext3 being the current standard). An ext4 file system can be mounted as an ext3 file system. However, if you want to use new ext4 features (called *extents*), mount it as an ext4 device (`mount -t ext4 /dev/DEVICE`). See the Ext4 FAQ for information on creating and working with ext4 file systems:

http://ext4.wiki.kernel.org/index.php/Frequently_Asked_Questions

A how-to document helps you get started with ext4 file systems:

http://ext4.wiki.kernel.org/index.php/Ext4_HowTo

You can convert an ext3 file system to ext4 by using a command like the following:

```bash
# tune2fs -O extents -E test_fs /dev/DEVICE
```

And, you can adjust the inode setting, for example, from 128 to 256, to improve efficiency with a command like the following:

```bash
# tune2fs -I 256 /dev/DEVICE
```

Encrypted file systems can be used to protect your data if your computer should become lost or stolen. In particular, this feature was created with laptops in mind. Someone stealing your laptop would not be able to mount or access data on an encrypted file system without your password. The *cryptsetup* command from the cryptsetup-luks package is used to create cryptographic volumes. Any file system, other than root (/), can be encrypted.

In addition, you can use encryption on hotpluggable file systems. A handy getting-started document appears at *http://flyn.org/eascrypto/eascrypto.html*. Another document relating directly to encrypting your file system on CentOS can be found at *http://wiki.centos.org/HowTos/EncryptedFilesystem*.

You can use *dm-crypt*, short for *device mapper encryption*, to provide transparent encryption to block devices, such as disks. By *transparent*, this means that programs don't need to worry that the contents of your disk are encrypted, as the mapping layer adds this feature. This allows you to work with word processors, text editors, drawing programs, and so on, without messing with encryption. But your files are stored safely protected (well, as safe as current encryption technology can be).

To use *dm-crypt*, you must have a 2.6 or higher Linux kernel with *dm-crypt* support. For more on *dm-crypt*, see *www.saout.de/misc/dm-crypt/*.

## Using the fstab File to Define Mountable File Systems

The hard disks on your local computer and the remote file systems you use every day are probably set up to mount automatically when you boot Linux. The definitions for which of these file systems are mounted are contained in the */etc/fstab* file. Here's an example of an */etc/fstab* file:

```text
/dev/VolGroup00/LogVol00 /
LABEL=/boot
        /boot    ext3    defaults    1 2
```

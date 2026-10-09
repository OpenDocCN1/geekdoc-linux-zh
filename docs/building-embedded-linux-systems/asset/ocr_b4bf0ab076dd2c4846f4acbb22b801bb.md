In this case, my target’s root filesystem is mounted via NFS, and I am running the MTD commands on my target.

Reading from a CFI MTD partition is no different from reading from any other device. The following command on my control module, for instance, will copy the binary image of the bootloader partition to a file:

```
$\ tt\ dd\ if=/dev/mtd0\ of=/tmp/ppcboot.img$
```

Since the bootloader image itself may not fill the entire partition, the ppcboot.img file may contain some extra unrelated data in addition to the bootloader image.

# # DiskOnChip

DiskOnChip devices used to be quite popular in x86-based embedded Linux systems, and the MTD subsystem goes a long way in providing support for them. I use it, for example, in my DAQ module. It remains that the DiskOnChip is a peculiar beast that requires an attentive master. The reasons for such a statement will become evident shortly.

The DiskOnChip is simply a NAND flash device with a user ASIC that performs ECC calculations in hardware. On that NAND flash, we use a special “translation layer” called NFTL, which works as a kind of pseudo filesystem that is used to emulate a normal hard drive. The underlying raw flash device is exposed as /dev/mtdN devices, while the emulated disk is exposed as /dev/nftlX. It is this dichotomy that often causes confusion.

Like all NAND flash devices, DiskOnChip devices can contain a certain number of manufacturing defects that result in bad blocks. Before a DiskOnChip is shipped from the factory, a Bad Block Table (BBT) is written on it. Although this table is not write-protected, it is essential to the operation of all software that reads and writes to the device. As such, M-Systems’s DiskOnChip software is capable of reading this table and storing it to a file. Linux should manage to preserve this table, but the tools are not particularly well tested.

There are two ways to install a bootloader on the DiskOnChip (DOC) and format it for NFTL. The first, which is most recommended by the MTD maintainer because it is guaranteed to preserve the Bad Block Table, is to use M-Systems’s DOS DOS utility. The second, which gives you the greatest degree of control over your DOC device from within Linux, is to use the doc_loadbios and nftl_format MTD utilities.

M-Systems’s DOS DOC tools and related documentation used to be available from the company’s website at http://www.m-sys.com. However, Sandisk bought M-Systems, and the website now redirects to the parent company. I have been unable to find the DiskOnChip tools on the new site.

When experimenting with a DiskOnChip, it is useful to save the Bad Block Table before you manage to destroy it. You can do this using the DOS format tool:
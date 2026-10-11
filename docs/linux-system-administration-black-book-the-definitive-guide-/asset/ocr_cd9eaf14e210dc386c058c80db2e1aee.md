+   2. Determine which media you want to use to store the particular backup segment in question, with the help of “Backup Hardware” in the In Depth section.

+   3. Which media you choose determines what software you need in order to create the backups. A map of which media requires which software is given in Table 3.9.

+   4. Load the kernel module or install the driver that you need for the media.

+   5. Install the software if necessary.

+   6. If you are using special software, read the documentation and learn how to use it. Otherwise, read the **tar** man page and see Chapter 4 for various tips on how to use the **tar** package.

+   7. Build your archive onto the media.

+   8. Verify that the archive worked. You know a backup worked if you are able to pull any files back off of the media. See the section “Restoring File Systems From Backup” for how to accomplish this task.

# Table 3.9 Drivers and outside software necessary for various backup media.

| Media | Driver | Software |
|---|---|---|
| CD writer or CD rewriter | cdrecord or cddaof | There are a number of programs out there that you can use to write the data to the CD. See the CD writer HOWTO at www.linuxdoc.org/HOWTO/CD-Writing-HOWTO-1.html for more information. |
| DVD writer or DVD rewriter | Universal Disk Format (UDF) file system driver, hardware driver | Program that can write to both ISO9660 and UDF. This technology is not quite ready for production use as yet. Watch your favorite Linux news sites for more information. |
| Floppy disk | No special drivers | No special software is necessary. |
| LS-120 | pf driver | No special software is necessary. |
| RAID | Kernel patch | Raidtools software. |
| Removable rack hard drive | No special drivers, but special equipment needed to swap things out | No special software is necessary. |
| Tape drive | ftape driver, which is already installed in most distributions | No special software is necessary, but sometimes it is worthwhile to have. |
| Zip disk | ppa driver (kernel module) | No special software is necessary. |
# Chapter 18: Ten Problem Areas and Solutions 289

```
ide3 master hdg
ide3 slave hdh
ide0 = primary controller
ide1 = secondary controller
ide2 = third controller
ide3 = fourth controller
```

# My CD-ROM Isn’t Detected

**Problem:** You're installing Linux, but it doesn’t find your CD-ROM.

**Solution:** Most newer CD-ROMs are either EIDE (ATAPI) or SCSI, and most newer computers have enough support to see either the ATAPI CD-ROMs or the SCSI CD-ROMs, so CD-ROM support is not quite the issue it was in the early days. In addition, some older systems and CD-ROMs are not supported.

Some early CD-ROMs pretended to be other devices (such as tape drives or floppies) to fool the computer into using them, but these CD-ROMs were hidden from the detection system. If your system is one of these, don't despair: You can supply information to help Linux find your CD-ROM.

First look at the preceding section about disk numbering. This will let you figure out the name Linux would call your CD-ROM if Linux knew about it. If you have an EIDE/ATAPI CD-ROM, type the following line whenever you see the boot or l1110 prompt while booting or installing your system:

```
linux hdx=cdrom
```

where $X$ is the number your CD-ROM would have if it could be detected.

# I Don’t Know How to Remove and Restore My MBR

**Problem:** You don’t know how to replace the boot record that was on your system before you installed Linux.

**Solution:** You can log in to Linux as *root* and then type the following command:
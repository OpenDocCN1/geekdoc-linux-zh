# 290 Part VI: The Part of Tens

```
/sbin/lilo -u
```

Another solution is to boot MS-DOS or Windows 3.1, 95, or NT to an MS-DOS prompt and type the following:

```
fdisk /mbr
```

# I Can't Use LILO to Boot

**Problem:** You need to put Linux on a disk or a partition that is beyond the 1023rd cylinder, the second IDE disk, or the second SCSI ID number, or you need to do something else that will make it difficult for Linux to booting LILO. Can you boot Linux in another way?

**Solution:** You can use a program called LOADLIN to boot from your MS-DOS or Windows system:

+   1. **Copy your configured Linux kernel to the C drive of your MS-DOS or Windows system.**

The easiest way to do this is to install Linux, log in as **root** and type the following:

```
grep image /etc/lilo.conf
```

A line similar to the following appears:

```
image=/boot/vmlinuz
```

This points to your compressed kernel, which in this example is located at /boot/vmlinuz.

+   2. **Copy the compressed kernel to a floppy disk, as follows:**
mccopy /boot/vmlinuz a:\vmlinuz.gz

The kernel name vmlinuz-2.0.36-0.7 refers to a specific version of the Linux kernel. Except for /boot/vmlinuz- part, which remains constant, the name might be slightly different on your system.

Now you have to copy LOADLIN from the *SuSE Linux For Dummies* CD-ROM in your CD-ROM drive.

+   3. MS-DOS or Windows and put the *SuSE Linux For Dummies* CD-ROM in your CD-ROM drive.

+   4. Go to the DOSUTILS directory and copy LOADLIN.EXE to your C drive:

If you are using MS-DOS or Windows 3.1, copy the LOADLIN16 file, which is the 16-bit version of the program.
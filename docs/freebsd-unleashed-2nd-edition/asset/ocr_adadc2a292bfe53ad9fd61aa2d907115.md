```
Format another (Y/N)? n

C:\>d:
D:\>cd tools
D:\TOOLS>copy fips.exe a:\
        1 file(s) copied
d:\TOOLS>copy restorerb.exe a:\
        1 file(s) copied
D:\TOOLS>copy errors.txt a:\
        1 file(s) copied
D:\TOOLS>
```

> NOTE
> You cannot use format a: /s to create a bootable floppy under Windows 2000 or XP. You will need to use Windows 95 or 98 for this task.

When you've created the bootable floppy, use it to reboot your system. After the system has finished booting, type **fips** at the DOS prompt to start the FIPS program.

# Working with FIPS

When FIPS first starts, it gives you a warning about not using it in a multitasking environment, among other things. Once you have read all the information, press any key to continue. If you have more than one hard disk in your system, FIPS will ask you which one you want to work on. Select the disk you want. FIPS will then show you the partition table of your disk. It will look something like the following:

```
        |           |    Start      |            End          |  Start |Number of|
Part.|bootable|Head Cy1. Sector|System|Head Cy1. Sector| Sector |Sectors  |  MB
------+----------+--------------+----------+-------------+--------+---------+
    1 |  yes    |    1        0 |   06h |     12     983  |   32   |    32   |  409312 |  199
    2 |  no     |    0        0 |   00h |      0       0   |   0    |     0   |     0   |    0
    3 |  no     |    0        0 |   00h |      0       0   |   0    |     0   |     0   |    0
    4 |  no     |    0        0 |   00h |      0       0   |   0    |     0   |     0   |    0

Checking root sector ... OK

Press any Key
```

If you have more than one partition on your disk, FIPS asks you to select which one you want to split. If you only have one partition on your disk, you are asked to press any key,
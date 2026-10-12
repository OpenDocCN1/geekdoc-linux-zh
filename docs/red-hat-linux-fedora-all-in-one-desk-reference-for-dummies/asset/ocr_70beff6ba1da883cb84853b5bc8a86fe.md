Figure 3-5 illustrates the device-naming convention for the floppy-drive device. As shown in Figure 3-5, you use the following command to format a 3.5-inch, high-density floppy disk in your system's A drive:

```
fdformat /dev/fd0H1440
```

# 2. Use the mformat command to put an MS-DOS file system on the low-level-formatted floppy disk.

If the floppy is in drive A, type the following command to create a formatted DOS floppy:

```
mformat a:
```

![](bbox=[0.25, 0.45, 0.85, 0.9])

Figure 3-5:
Here's how you can construct the name of a floppy disk drive in Red Hat Linux.

3 or 4 digits indicating capacity of floppy disk in kilobytes:
5.25-inch: 360, 720, or 1200
3.5-inch: 360, 720, or 1440

One of the following letters:
d = low-density 5.25-inch
D = low-density 3.5-inch
h = high-density 5.25-inch
H = high-density 3.5-inch

One of the following letters:
0 = first floppy drive (A:)
1 = second floppy drive (B:)
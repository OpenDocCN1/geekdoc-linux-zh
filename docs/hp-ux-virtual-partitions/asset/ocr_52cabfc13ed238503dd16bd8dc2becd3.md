```
00032 /dev/dsk/c9t0d0   00032 current
·
·
·
08733 /dev/dsk/c8t0d1   01729 current
08734 /dev/dsk/c8t0d1   01730 current
08735 /dev/dsk/c8t0d1   01731 current
08736 /dev/dsk/c8t0d1   01732 current
08737 /dev/dsk/c8t0d1   01733 current
08738 /dev/dsk/c8t0d1   01734 current
08739 /dev/dsk/c8t0d1   01735 current
08740 /dev/dsk/c8t0d1   01736 current
08741 /dev/dsk/c8t0d1   01737 current
08742 /dev/dsk/c8t0d1   01738 current
08743 /dev/dsk/c8t0d1   01739 current
08744 /dev/dsk/c8t0d1   01740 current
08745 /dev/dsk/c8t0d1   01741 current
08746 /dev/dsk/c8t0d1   01742 current
08747 /dev/dsk/c8t0d1   01743 current
08748 /dev/dsk/c8t0d1   01744 current
08749 /dev/dsk/c8t0d1   01745 current
08750 /dev/dsk/c8t0d1   01746 current
08751 /dev/dsk/c8t0d1   01747 current
08752 /dev/dsk/c8t0d1   01748 current
08753 /dev/dsk/c8t0d1   01749 current
08754 /dev/dsk/c8t0d1   01750 current
```

This listing has been abbreviated where the three dots are shown. Only the beginning of the first disk and end of the last disk are shown. The **lvdisplay** does indeed show the five primary disks of which the logical volume is comprised.

The final step is to place a file system on the logical volume we set up in vgn00. This is a task for which *SAM* is ideally suited. Figure 9-2 shows the *SAM* screen shot of the logical volumes we created. There is one logical volume created for each of the ten volume groups.
+   - Noname (Section D.5.7)
+   - AlphaPC64 (Section D.5.7)
+   - EB164 (Section D.5.7)
+   - PC164 (Section D.5.7)

# D.5.7 System Specific Information

**AxpPC133 (Noname)**

The Noname board can load MILO from the Windows NT ARC firmware (Section D.5.1), from the SRM Console (Section D.5.6). and from a failsafe boot block floppy (Section D.5.4). A flash management utility, runnable from MILO is available so that once MILO is running, it can be blown into flash (Section D.7). However, be warned that once you have done this you will lose the previous image held there as there is only room for one image.

The way that Noname boots is controlled by a set of jumpers on the board, J29 and J28. These look like:

```
```text
       4
J29    2 x x x 6
       1 x x x 5

J28    2 x x x 6
       1 x x x 5
       3
```
```

The two options that we're interested in are J28, pins 1-3 which boots the console/loader from flash and J29, pins 1-3 which boots the console/loader from a boot block floppy. The second option is the one that you need to first boot MILO on the Noname board.

Once you've selected the boot from floppy option via the jumpers, put the SRM boot block floppy containing MILO into the floppy and reboot. In a few seconds (after the floppy light goes out) you should see the screen blank to white and MILO telling you what's going on.

If you are really interested in technical stuff, the Noname loads images off of the floppy into physical address 0x104000 and images from flash into
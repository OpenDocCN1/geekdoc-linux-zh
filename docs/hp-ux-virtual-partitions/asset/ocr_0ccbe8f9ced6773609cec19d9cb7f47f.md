![](bbox=[0.28, 0.13, 0.75, 0.155])

Get a snapshot of existing configuration and save output to directory.
```shell
# lscan -funC.disk     # hdfl
# vgdisplay -v         # swapinfo
# lvdisplay -v /dev/vg00/lv0* # lvboot, /dev/vg00
# 0 /dev/vg00*         # hdic, -cb, /dev/dsk/c0t0d0
```

Reduce mirror of all logical volumes in /dev/vg00 to zero.
```shell
# lvreduce -n 0 /dev/vg00/lv0*  thru  lv07
```

Check to see that “Mirror copies” is equal to zero (v- option not required).
```shell
# lvdisplay /dev/vg00/lv0* -v more
```

Remove /dev/dsk/c0t5d0 from vg00, this was mirror of /dev/dsk/c0t6d0.
```shell
# vgreduce /dev/vg00 /dev/dsk/c0t5d0
```

Verify c0t5d0 is removed with vgdisplay -v.
PV Name /dev/dsk/c0t5d0 should no longer appear in listing, only c0t6d0.
```shell
# vgdisplay -v
```

Verify that “dump lv0” is in /stand/system. If not, add it and reconfigure kernel using procedure in 11.x System administration book.

Perform hardware upgrade: 4 GByte disk /dev/dsk/c0t5d0 at 100.5.0
becomes: /dev/dsk/c11t0 / 10043.5.0; add new 2 GByte disk for dump
only purposes at /dev/dsk/c0t5d0 at 100.5.0.

After reboot, verify that new disks are in place at proper addresses with
lscan.
```shell
# lscan -funC.disk
```

Use vgdisplay to see that c0t6d0 is only disk in vg00 and other volume
groups are unchanged.
```shell
# vgdisplay -v /dev/vg00
# vgdisplay -v /dev/vg-other>
```

# Figure 9-13  Disk Reconfiguration Flow Diagram - Part 1 (Rearrange Disks)
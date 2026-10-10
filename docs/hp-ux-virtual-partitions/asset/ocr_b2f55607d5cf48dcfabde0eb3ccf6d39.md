# F5

At this point `c0t5d0` is no longer in `vg00`. Verify that "PV Name" `c0t5d0` is no longer in `vg00` with `vgdisplay`.

```
# vgdisplay -v
```

There should be no `c0t5d0` in `vg00`.

# F6

Verify that "dump Ivol" is in /stand/system. If not, add "dump vol" and reconfigure the kernel. See the kernel rebuild procedure in Chapter 1.

# F7

Now the hardware upgrade takes place. The system is shut down, disk drives are added and moved, and the system is rebooted. The 4 GByte disk `/dev/dsk/c0t5d0` becomes `/dev/dsk/c1t3d0` at address 10/4/4,3.0, and a new 2 GByte disk is introduced as 10/0,5.0 with the device name `/dev/dsk/c0t5d0`. The second half of Figure 9-4 depicts this change.

# F8

The first activity to perform after the hardware upgrade is to view the new disks with `ioscan`. There is now a 2 GByte disk at 10/0,5.0 and a 4 GByte disk at 10/4/4,3.0.

```
# iscan -func disk
```

| Class | I | H/W Path | Driver | S/W State | H/W Type | Description |
|---|---|---|---|---|---|---|
| disk | 2 | 10/0,5.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST332555W |
| disk | 3 | 10/0,6.0 | sdisk | CLAIMED | DEVICE | SEAGATE ST31550W |
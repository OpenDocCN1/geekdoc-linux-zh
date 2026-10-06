# # Chapter 10 • PROVIDING HIGH AVAILABILITY IN YOUR UNIX SYSTEM

# maintainit d10 -m d11
d10: Mirror is setup
# metattach d10 d12
d10: Submirror d12 is attached

After synchronization is complete, you can check the status of the mirror using the metastat command:

```
# metastat d10
d10: Mirror
Submirror 0: d11
State: Okay
Submirror 1: d12
State: Okay
Pass: 1
Read option: roundrobin (default)
Write option: parallel (default)
Size: 1027216 blocks
```

```
d11: Submirror of d10
State: Okay
Size: 1027216 blocks
Stripe 0:
| Device | Start Block | Dbase State | Hot Spare |
| c0tid0s0 | 0 | No | Okay |
```

```
d12: Submirror of d10
State: Okay
Size: 1027216 blocks
Stripe 0:
| Device | Start Block | Dbase State | Hot Spare |
| c0tid0s0 | 0 | No | Okay |
```

# Use Identical Disks in RAID Arrays

Try to use disks of the same capacity when mirroring. If this isn't possible, the total size will be the size of the smallest disk, and this wastes space on the larger disks. This is true for RAID-1 in general, not just DiskSuite. Striped RAID levels (RAID-0, RAID-4, and RAID-5) have even stricter requirements. For more details, see Chapter 11 in the section "Stripe Data Across Multiple Disks."

The GUI interface metastatool is just as flexible as the command line. Graphical output analogue to the metastat d10 command is shown in Figure 10.11.

![](bbox=[0.078, 0.633, 0.115, 0.666])
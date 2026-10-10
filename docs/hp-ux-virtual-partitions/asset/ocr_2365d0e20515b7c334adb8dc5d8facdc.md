```
# vgcfgrestore - /dev/vgXX /dev/rdsk/ext0xd  ; volume group configuration restore
# vgchange -a y /dev/vgXX                         ; change volume group to available (-a y)
# vgsync /dev/vgXX                                 ; resync logical volumes in volume group
# mkboot /dev/rdsk/ext0xd                          ; create boot area on disk
# mkboot -a "hpux 1q" /dev/rdsk/ext0xd             ; specify low quorum in boot area
# shutdown <desired options>                        ; reboot system to take effect

vgcfgbackup is run automatically
```

Notes:

Confirm you have *etc/lvmconf/vgXX.conf*

Defective disk was mirrored before it failed

Additional steps may be required on your system

Figure 9-8 Replace a Mirrored Disk Boot Disk

In this example, we performed the same first three steps as in the previous example, but we also have to create a boot area on the disk. The system has to be rebooted in order for this to take effect.

In Figure 9-9, we want to move a volume group onto a different system.
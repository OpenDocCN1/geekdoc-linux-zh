The next step is to initialize the partition for LVM. The tool to use is **pvcreate**:

```
dalo:~ # pvcreate /dev/hda9
Physical volume "/dev/hda9" successfully created
```

**pvscan** shows the physical volumes and their use:

```
dalo:~ # pvscan
PV /dev/hda9 lvm2 [242,95 MB]
Total: 1 [242,95 MB] / in use: 0 [0 ] / in no VG: 1 [242,95 MB]
```

The tool **pvmove** is used to move data from one physical volume to another (providing there is enough space), in order to remove a physical volume from LVM.

# ### Tools to Administer Volume Groups

The tool **vgcreate** is used to create a new volume group. To create the volume group *system*, and add the physical volume /dev/hda9 to it, enter:

```
dalo:~ # vgcreate system /dev/hda9
Volume group "system" successfully created
dalo:~ # pvscan
PV /dev/hda9 VG system lvm2 [240,00 MB / 240,00 MB free]
Total: 1 [240,00 MB] / in use: 1 [240,00 MB] / in no VG: 0 [0 ]
```

pvscan shows the new situation. To add further physical volumes to the group, use **vgexpand**. Removing unused physical volumes is done with **vgreduce** after shiting data from the physical volume scheduled for removal to other physical volumes using pvmove. **vgremove** removes a volume group, providing there are no logical volumes in the group.

**1 HARDCOPY PERMITTED-NO DISTRIBUTION ALLOWED**
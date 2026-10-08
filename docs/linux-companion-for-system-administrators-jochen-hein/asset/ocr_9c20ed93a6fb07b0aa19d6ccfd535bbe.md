# 114 CONFIGURATION AND ADMINISTRATION

```
# lvcreate -n tmplv -L 128M rootvg
lvcreate -- doing automatic backup of "rootvg"
lvcreate -- logical volume /dev/rootvg/tmplv
successfully created
# mkefs /dev/rootvg/tmplv
# mkefs 1.17, 26-Oct-1999 for EXT2 FS 0.5b, 95/08/09
# mount /dev/rootvg/tmplv/mnt

# umount /mnt
# lvremove /dev/rootvg/tmplv
# lvremove -- do you really want to remove "dev/rootvg/tmplv"
Cy/n:
lvremove -- doing automatic backup of volume group "rootvg"
lvremove -- logical volume /dev/rootvg/tmplv"
successfully removed
```

**Listing 4.23** Logical volumes with lvcreate.

You will find an overview of how LVM works in Figure 4.2 which shows a volume group consisting of three physical volumes. The shaded section is a logical volume that is stored over several physical volumes – transparent user. The smallest part that can be used for storage is the physical extent. You may define that size when creating the volume group. The default value is 4 MB, but you can have powers of two between 8 KB and 512 MB. This number restricts the maximum size of a volume group.

![](bbox=[0.335, 0.635, 0.875, 0.815])

**Figure 4.2** A small volume group.

The gain for the system administrator is that he/she may extend a logical volume as long as there is free space in the volume group. And even if the volume
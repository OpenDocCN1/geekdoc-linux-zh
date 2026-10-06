# CHAPTER 7 File Systems 205

Substituting the correct values in this command, this type:

```
[root@fedora-server ~]# vgxtend fedora /dev/sda3
Volume group "fedora" successfully extended
```

+   3. View your changes with the vgdisplay command:
[root@fedora-server ~]# vgdisplay
--
Volume group --
VG Name fedora
..<OUTPUT TRUNCATED...>
Act PV 2
VG Size 99.06 GiB
PE Size 4.00 MiB
Total PE 25360
Alloc PE / Size 19075 / 74.51 GiB
Free PE / Size 24.55 GiB
VG UUID cLNaj-awty-0xIEhNEY-tNsc-6n1d-yFXwD

Note that the VG Size, Total PE, and Free PE values have dramatically increased. We have a total of 6285 PEs (or 24.55 GiB).

# Creating a Logical Volume

Now that we have room in the VG, we can go ahead and create the logical volume (LV).

+   1. First view the current LVs on the system:
[root@fedora-server -]# lvsdisplay
--
Logical volume --
LV Path /dev/fedora/root
LV Name root
VG Name fedora
..<OUTPUT TRUNCATED...>
--
Logical volume --
LV Path /dev/fedora/swap
LV Name swap
VG Name fedora
..<OUTPUT TRUNCATED...>
--
Logical volume --
LV Path /dev/fedora/home
LV Name home
VG Name fedora
..<OUTPUT TRUNCATED...>
--
Logical volume --
LV Path /dev/fedora/tmp
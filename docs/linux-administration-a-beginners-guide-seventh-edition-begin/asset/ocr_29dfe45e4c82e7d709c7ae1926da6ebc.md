# 206 Linux Administration: A Beginner's Guide

| LV Name | tmp |
| VG Name | fedora |
| ...<<OUTPUT TRUNCATED>... |

The preceding output shows the current LVs:

+   - /dev/fedora/root
- /dev/fedora/swap
- /dev/fedora/home
- /dev/fedora/tmp

2. With the background information that we have now, we will create an LV using the same naming convention (that is, name of mount point) currently used on the system. We will create a fifth LV called **var** on the **fedora** VG.
The full path to the LV will be `/dev/fedora/var`. Type the following:

```
```
root@fedora-server -]# lvcreate -l 6285 --name var fedora
Logical volume "var" created
```
```

> **NOTE** You can activate your LV any way you want. We named ours **var** for consistency only. We could have replaced **var** with another name, such as "my-volume" or "LogVol04" if we wanted.
The --name (-n) option determines the name of the LV.
The -l option specifies the size in physical extents (see Step 1 under 'Assigning a Physical Volume to a Volume Group').
We could also specify the size in gigabytes or megabytes by using an option such as **-L 19.03G** or **-L 19030M.**

3. View the LV you created:

```
```
root@fedora-server -]# lvdisplay /dev/fedora/var
--- Logical volume ---
LV Path           /dev/fedora/var
LV Name           var
VG Name           fedora
...<<OUTPUT TRUNCATED>...
LV Size           24.55 GiB
Current LE       6285
```
```
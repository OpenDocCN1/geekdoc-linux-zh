# Adding and Managing RHEL 9 Swap Space

|  |  |
|---|---|
| Segments | 1 |
| Allocation | inherit |
| Read ahead sectors | auto |
| - currently set to | 256 |
| Block device | 253:1 |

Clearly, the swap resides on a logical volume named swap00 which is part of the volume group named rhel. The next step is to verify if there is any space available on the volume group that can be allocated to the swap volume:

```
```
# vgs
  VG   #PV #LV #SN Attr   VSize   VFree
  rhel   2   3   0 wz--n- 197.66g <22.00g
```
```

If the amount of space available is sufficient to meet additional swap requirements, turn off the swap and extend the swap logical volume to use as much of the available space as needed to meet the system's swap requirements:

```
```
# swapoff /dev/rhel/swap
# lvextend -L+8GB /dev/rhel/swap
  Logical volume rhel/swap successfully resized.
```
```

Next, reformat the swap volume and turn the swap back on:

```
```
# mkswap /dev/rhel/swap
mkswap: /dev/rhel/swap: warning: wiping old swap signature.
Setting up swapspace version 1, size = 12 GiB (12754874368 bytes)
no label, UUID=241a4818-e51c-4b8c-9bc9-1697fc2ce26e

# swapon /dev/rhel/swap
```
```

Having made the changes, check that the swap space has increased:

```
```
# swapon
NAME      TYPE      SIZE USED PRIO
/dev/dm-1 partition 12G  0B   -2
```
```

# 33.7 Adding Swap Space to the Volume Group

In the above section, we extended the swap logical volume to use space already available in the volume group. If no space is available in the volume group, it must be added before extending the swap.

Begin by checking the status of the volume group:

```
```
# vgs
  VG     #PV #LV #SN Attr   VSize   VFree
  rhel     1   3   0 wz--n- <297.09g     0
```
```

The above output indicates that no space is available within the volume group. However, suppose
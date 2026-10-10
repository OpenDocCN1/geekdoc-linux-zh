# F24

Remove the boot area entirely from **vg00** with lvmboot.

```
# lvmboot -r /dev/vg00
```

# F25

Verify that the boot area was removed with lvmboot.

```
# lvmboot -v
```

Boot Definitions for Volume Group /dev/vg00: The Boot Data Area is empty.

# F26

Assign the root logical volume to **lvoll** on /dev/vg00 with lvmboot.

```
# lvmboot -r lvoll /dev/vg00
```

# F27

Assign the swap to **lvol2** on /dev/vg00.

```
# lvmboot -s lvol2 /dev/vg00
```

```
# swapinfo
```

```
     Kb        Kb        Kb     PCT START/    Kb
TYPE    AVAIL   USED     FREE    USED LIMIT RESERVE PRI NAME
dev     512000      0    512000   0%    0        -   1 /dev/vg00/lvol2
reserve -      23144   -23144             -
memory  1671008 27328  1643680  2%
```


# F28

Assign the dump to the logical volume **dump** on /dev/vg00.

```
# lvmboot -d dump /dev/vg00
```
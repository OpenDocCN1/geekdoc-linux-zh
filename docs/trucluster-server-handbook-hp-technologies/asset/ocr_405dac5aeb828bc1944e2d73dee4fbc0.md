Edit the label.

```
perl -i -pe 's/15667864/1572864/' boot_partition.lbl
perl -i -pe 's/0/256/' boot_partition.lbl
perl -i -pe 's/4093656/0/' boot_partition.lbl
```

```
grep -v 'stanza' boot_partition.lbl
# partition     offset    fs_type  size  size  cpg  #  *CYL values
  a:             524288          0       AdvFS              * 0 - 156*
  b:            1572864     524288  unused      0     0    * 156* - 622*
  c:           17773524          0  unused      0     0    * 0 - 5289*
  d:                  0          0  unused      0     0    * 0 - 0*
  e:                  0          0  unused      0     0    * 0 - 0*
  f:                  0          0  unused      0     0    * 622* - 624*
  g:            15674324     2097152  AdvFS              * 624* - 5289*
  h:                2048    17771476  cnx                 * 5289* - 5289*
```

Put the label back on the member’s root disk.

```
disklabel -rw advfs disk2 boot_partition.lbl
```

+   8. Allow the member to start using the swap partition.

```
swapon -a /dev/disk/dsk2b
```

+   9. Add the vm:swapdevice attribute to the member’s sysconfigtab file.

```
cat > swap_noXLm.stanza
vm:
        swapdevice = /dev/disk/dsk2b
^D
```

```
sysconfigdb -m -f swap_noXLm.stanza vm
```
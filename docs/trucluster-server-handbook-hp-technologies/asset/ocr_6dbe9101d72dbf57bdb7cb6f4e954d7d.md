```
```shell
# clu_get_info | grep dak
Quorum disk : sdb4
```
```

+   - Check the device's disk label using the disklabel(8) command to see which partitions are unused and whether or not the partition you have in mind overlaps an “in use” partition.

```
```text
# disklabel sds | grep -E "8 part"
8 partitions:
  size        offset    fstype  fsize  bsize  cpg  # cyl  values
 a:  2933672         0    4.2BSD   1024   8192   16  #  0 - 385*
 b:  3490644    1293637    unused      0      0    #  385* - 1557*
 c:  1773524         0    unused      0      0    #  0 - 5289*
 d:  3389144    5234331    unused      0      0    #  1557* - 2566*
 e:  4180140    8623475    unused      0      0    #  2566* - 3810*
 f:  4969099   12893615    unused      0      0    #  3810* - 5289*
 g:  5959156     5234331    unused      0      0    #  1557* - 3331*
 h:  6580037   11193487    unused      0      0    #  3331* - 5289*
```
```

+   - Check the /etc/fdmns subdirectories. These subdirectories contain symbolic links to the devices used by the AdvFS domains on the cluster. Do you remember the fln Korn shell function we created in chapter 6? If not, you can use an ls(1) command piped into the awk(1) command for this example or turn to chapter 6 and check it out.

```
```shell
# ls /etc/fdmns/* | sort | uniq

dsk0a -> /dev/disk/dsk0a
dsk0g -> /dev/disk/dsk0g
dsk1a -> /dev/disk/dsk1a
dsk1g -> /dev/disk/dsk1g
dsk1h -> /dev/disk/dsk1h
dsk2a -> /dev/disk/dsk2a
dsk2a -> /dev/disk/dsk2a
dsk6c -> /dev/disk/dsk6c
dsk7a -> /dev/disk/dsk7a
dsk7g -> /dev/disk/dsk7g
dsk7h -> /dev/disk/dsk7h
dsk8a -> /dev/disk/dsk8a
dsk8h -> /dev/disk/dsk8h
```
```

The equivalent ls and awk commands are:

```
```shell
# ls -l /etc/fdmns/* | awk '{ print $9,$10,$11 }' | sort | uniq
```
```

or:
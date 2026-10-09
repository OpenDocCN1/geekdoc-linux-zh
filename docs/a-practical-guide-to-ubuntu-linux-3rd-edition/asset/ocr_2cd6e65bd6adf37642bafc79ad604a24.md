# parted: REPORTS ON AND PARTITIONS A HARD DISK

The `parted` (partition editor) utility reports on and manipulates hard disk partitions. The following example shows how to use `parted` from the command line. It uses the `print` command to display information about the partitions on the `/dev/sda` drive:

```
```
$ sudo parted /dev/sda print
Disk geometry for /dev/sda: 0kB - 165GB
Disk label type: msdos
Number Start   End     Size    Type     File system  Flags
1      32kB    1045MB  1045MB  primary  ext4         boot
2      1045MB  12GB    10GB    primary  ext4
3      12GB    22GB    10GB    primary  ext4
4      22GB    165GB   143GB   extended
5      22GB    23GB    1045MB  logical  linux-swap(v1)
6      23GB    41GB    18GB    logical  ext4
7      41GB    82GB    41GB    logical  ext4
```
```

Figure 16-5 graphically depicts the partitions shown in this example. The first line that `parted` displays specifies the device being reported on (`/dev/sda`) and its size (165 gigabytes). The `print` command displays the following columns:

# Figure 16-5 The primary and extended partitions from the example

![](bbox=[0.3, 0.09, 0.9, 0.37])

```
```
31327  zach     18  0  2092  596  492 R  57  0.0  0:00.92  cp
31311  root     15  0    0    0   0 S  16  0.0  0:00.38  pdf
6870   zach     27  12  331m  190m  37m R  2   9.4  1:95:42.98 firefox-bin
31303  root     15  0    0    0   0 S  2   0.0  0:00.42  pdf
...   1 root     15  0  2912  1808  488 S  0   0.1  0:01.55  init
```
```
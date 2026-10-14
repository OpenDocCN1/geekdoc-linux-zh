```
500 10000 1000000000 ext3 \
  method{ format } format{ } \
  use_filesystem{ } filesystem{ ext3 } \
  mountpoint{ / } \
. \
64 512 300% linux-swap \
  method{ swap } format{ } \
.
```

Note that this entire configuration is intended to appear on a single line, so to make it more readable you are allowed to use the \ symbol at the end of the line to extend your options to multiple lines, as with shell scripts.

The first line labels this recipe as boot-root, and all of the rest of the lines are considered part of the boot-root recipe. The way that the lines are formatted separates each of the three partitions from the others. First let’s take a closer look at the /boot partition:

```
40 50 100 ext3 \
  $primary{ } $bootable{ } \
  method{ format } format{ } \
  use_filesystem{ } filesystem{ ext3 } \
  mountpoint{ /boot } \
.
```

The first line has four different fields corresponding to the minimal size of the partition, the priority, the maximal size, and the parted-style file system. All disk sizes in this file are in megabytes, so here we would have a disk that is at least 40Mb but if available could grow up to 100Mb, and it is a standard Linux partition with an ext3 file system. If you compare this line with the corresponding line for the swap partition, you will notice that for its maximal field it uses 300%. When a percentage is used, the size is determined based on the amount of RAM on the system. What 300% means in this case is that the swap partition’s maximal size will be 300% of the amount of RAM on the machine.

The priority field deserves a little extra description. It also represents a partition size in megabytes and usually is set to some value between the minimal and maximal values. The installer uses the priority setting of each partition when it decides how much of the available space to give each partition. The higher the priority compared to that of other partitions, the
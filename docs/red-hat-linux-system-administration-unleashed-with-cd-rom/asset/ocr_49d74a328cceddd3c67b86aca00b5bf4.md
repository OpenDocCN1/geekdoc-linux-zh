The syntax of the partition file is critical to the proper operation of this script. This file is used to build the input file to the sfdisk command. Each line consists of a device name, a start point, the size in megabytes for the partition, the partition type, a flag indicating whether the partition should be marked active or not, and finally, the eventual mount point and a sequence number indicating the order in which they should be mounted. Following is a sample partition file. Note that in this file, you specify a /dev/sda4 partition, but give it no values. This is required to satisfy the sfdisk command.

```
1,1024,L,*,/,1
2,128,S,,,
3,,E,,,
4,,,
5,1024,L,/,usr,2
6,,L,,/var,3
```

This sample file above creates a partition on /dev/sda1 of 1024 megabytes, with a type of L (for Linux native), and marks it active. It then creates a type S, or swap partition, of 128 megabytes on /dev/sda2. The next partition is of type E, or extended, and because no size was specified, takes up the remainder of the disk. Now you specify /dev/sda4, which has no values for size, start, or type. This partition does not really exist, but must be specified to satisfy sfdisk. The next real partition is /dev/sda5, which is a logical drive of type L that is 1024 megabytes in size. The final partition is /dev/sda6, which is also type L and takes up the remainder of the extended partition. Using this sample partition file and the script in Listing 3.2 generates the following output:

```
[root@quicksilver chapter3]# ./dprepare -t nomad -b hda -p partfile

Disk /dev/hda: 128 heads, 63 sectors, 785 cylinders

Old situation:
Units = megabytes of 1048576 bytes, blocks of 1024 bytes, counting from 0

Device Boot Start End MB #blocks Id System
/dev/sda1 0* 1536- 1536- 1572448* b Win95 FAT32
/dev/sda2 * 1535+ 3027- 1493- 1528128 83 Linux
/dev/sda3 3027+ 3090- 63 64512 82 Linux swap
/dev/sda4 0 - 0 0 0 Empty
New situation:
Units = megabytes of 1048576 bytes, blocks of 1024 bytes, counting from 0

Device Boot Start End MB #blocks Id System
/dev/sda1 * 0+ 1027- 1028- 1052351* 83 Linux
/dev/sda2 1027+ 1157- 130- 133056 82 Linux swap
/dev/sda3 1157+ 3090- 1934- 1978212 5 Extended
```
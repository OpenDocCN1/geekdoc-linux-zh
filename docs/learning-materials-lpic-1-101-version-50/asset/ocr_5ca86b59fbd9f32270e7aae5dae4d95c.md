of all the valid codes by using the command 1.  

do not confuse the partition type with the file system used on it. Although at first there was a relation between them, today you cannot assume this to be true. A Linux partition, for example, can contain any Linux-native file system, like ext4 or ReiserFS.

> **TIP**  
> Linux partitions are type 83 (Linux). Swap partitions are type 82 (Linux Swap).

# # Managing GUID Partitions with GDISK

The utility gdisk is the equivalent of fdisk when dealing with GPT partitioned disks. In fact, the interface is modeled after fdisk, with an interactive prompt and the same (or very similar) commands.

# ## Printing the Current Partition Table

The command p is used to print the current partition table. The output is something like this:

```
```
Command (? for help): p
Disk /dev/sdb: 3903578 sectors, 1.9 GiB
Model: DataTraveler 2.0
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): AB41B5AA-A217-4D1F-8200-E062C54285BE
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 3903544
Partitions will be aligned on 2048-sector boundaries
Total free space is 1282071 sectors (626.0 MiB)

Number  Start (sector)    End (sector)      Size       Code  Name
     1          2048        2099199      1024.0 MiB   8300  Linux file
     2        2623488       3147775       256.0 MiB   8300  Linux file
```
```

Right from the start, we notice a few different things:

+   1. Each disk has a unique Disk Identifier (GUID). This is a 128 bit hexadecimal number, assigned randomly when the partition table is created. Since there are $3.4 \times 10^{38}$ possible values to this number, the chances that 2 random disks have the same GUID are pretty slim. The GUID can be used to identify which file systems to mount at boot time (and where), eliminating the need to use the device path to do so (like /dev/sdb).
+   2. See the phrase **Partition table holds up to 128 entries**? That's right, you can have up to 128 partitions on a GPT disk. Because of this, there is no need for *primary* and *extended*
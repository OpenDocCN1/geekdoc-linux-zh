v.4.33

A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

# Starting with fdisk:

root@forensic1:/home/barry/able_3# fdisk -l able_3.raw
Disk able_3.raw: 4 GiB, 429496296 bytes, 8388608 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: gpt
Disk identifier: B94F8C48-6CE1-43F4-A062-AA2AE55C2C83

```
Device Start End Sectors Size Type
ableable_3.raw1 2048 104447 102400 50M Linux filesystem
ableable_3.raw2 18448 204800 100M Linux filesystem
ableable_3.raw3 57192 8388574 7817183 3.7G Linux filesystem
```

Looking at the output, we see that there is a GPT partitioning scheme. You could re-run the command using gdisk for documentation purposes. Once you've finished with fdisk, exit the root login and you are back to a normal user:

```
root@forensic1:/home/barry/able_3# exit
logout
```

```
barry@forensic1:-$3$
```

Let's go ahead and dd out each partition. With the output of fdisk -l shown above, the job is easy.

```
barry@forensic1:-$3$ dd if=able_3.raw of=able_3.part1.raw bs=512 skip=2048
count=102400
102400+0 records in
102400+0 records out
52428800 bytes (52 MiB, 50 MiB) copied, 0.167642 s, 313 MB/s
barry@BlackBuilds:-$able_3$ dd if=able_3.raw of=able_3.part2.raw bs=512
skip=104448 count=204800
204800+0 records in
204800+0 records out
104857600 bytes (105 MiB, 100 MiB) copied, 0.385551 s, 272 MB/s
barry@BlackBuilds:-$ dd if=able_3.raw of=able_3.part3.raw bs=512
skip=571392 count=7817183
7817183+0 records in
7817183+0 records out
4002397696 bytes (4.0 GiB) copied, 94.3723 s, 42.4 MB/s
```

200
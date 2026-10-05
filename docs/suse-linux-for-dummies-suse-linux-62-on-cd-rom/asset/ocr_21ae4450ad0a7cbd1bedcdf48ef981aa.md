# Part IV: Maintaining Your System

line up properly, so more cars may try to go through onebooth (probably
the next to the combination information booth and liquor store) than
tother tollbooth.

Having one disk on your system is like having one tollbooth on the highway.
All I/O on your system (including paging and swapping) goes out to disk.
If you have two disks, some I/O load might go to one disk and some to the
other. Although the proportions of data flowing to each disk may change over
time, it would be nice if, on average, half the data was going to one disk and
half to the other.

To try to accomplish this, some systems administrators put separate sys-
tems on different disks and separate the file systems across disk drives. For
example, suppose you broke up the disks into the following directories and
made a file system for each one:

```
/
/tmp
/usr
/usr/tmp
/home
```

You may find that under a normal load, data is written to each file system
equally.

Separating the swap areas onto another disk means that even more I/O load
dis distributed evenly. Think of it as having a mountain of backpacks to carry.
You can put them all on one poor, unsuspecting pack mule and watch its
kne buckle under the load, or you can distribute them to several pack
mules (but you have to manage them all as you trundle the trail).

Another reason for breaking up the data into separate file systems is what is
known as head contention. Disks having moving parts called disk heads that are
al like the heads of an audio cassette deck. To read or write data, the data
must pass underneath the heads. Unlike the heads in an audio cassette, the
disk heads don't touch the disk but float a very short distance above the sur-
face of the disk. Moving these heads from one place to another to real data
as slow process in computer time, and most people want to avoid them
unnecessarily. By having all the data on one disk, each program fights with the
other ones to move the heads where they should be for that program. By sep-
arating the data, you have a better chance that the data you want is close to
the previous data you requested and not clear across the disk.

procinfo tells you how many reads and writes you do per disk. Keeping an
ye on these numbers tells you how much data is being written to your disks
and how much the heads are moving. How can you tell your disk's peak
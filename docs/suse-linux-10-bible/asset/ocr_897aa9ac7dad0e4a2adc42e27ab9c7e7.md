excellent choice for most filesystems, especially user filesystems and mail or web server partitions where you will be creating and deleting large numbers of small files. As discussed earlier, the design of the ReiserFS makes it a fast filesystem in which to locate files also helps you get the most out of your available storage by handling small files (less than 4K).

Unfortunately, there is no automatic way to convert an existing filesystem of some other type to a ReiserFS. To convert an existing filesystem to ReiserFS, you would have to back up all data from one of your partitions, create a new ReiserFS partition on that partition, and then restore your data there.

List 3-9 shows (and related output) used to create a ReiserFS filesystem from scratch on /dev/hda5 using the default parameters. Although this example uses the mkfs.reiserfs command directly, you could do exactly the same thing by executing the command mkfs -t reiserfs /dev/hda5.

Listing 3-9: Creating a ReiserFS Filesystem

```
bible: # mkfs.reiserfs /dev/hda5
mkfs.reiserfs 3.6.13 (2003 www.namesys.com)
```

A pair of credits:
BigStorage (www.bigstorage.com) contributes to our general fund every month, and has so for quite a long time.

Alexander Lyman keeps our hardware running, and was very generous to our project in many little ways.

Guessing about default format.. Kernel 2.6.4-52-default is running.
Format 3.6 with standard journal
Count of blocks on the device: 48992
Number of blocks consumed by mkreiserfs formatting process: 8213
blockSize: 4096
Hash function used to sort names: "5"
Journal Size 8193 blocks (first block 18)
Journal max length 1024
inode generation number: 0
UUID: 47f2ca6a-3fc5-4097-bbc0-3124bc0c214a
ATTENTION: YOU SHOULD REBOOT AFTER DISK!
ALL DATA WILL BE LOST ON /dev/hda5!
Continue (y/n)
Initializing journal - 0%...20%...40%...60%...80%...100%
Syncing... .ckdone

ReiserFS is noticed, the creation of the ReiserFS filesystem makes doubly sure that you are aware that you will erase data on your partition once the filesystem
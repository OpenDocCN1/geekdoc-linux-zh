time you reboot the system and never checking them. It does so by scheduling when fsck checks a filesystem (these checks occur only when the system is booted).<sup>1</sup> You can use two scheduling parameters: time elapsed since the last check and number of mounts since the last check. The following command causes fsck to check /dev/sda5 after it has been mounted eight times or after 15 days have elapsed since its last check, whichever happens first:

```
$ sudo tune2fs -c 8 -i 15 /dev/sda5
tune2fs 1.41.11 (14-Mar-2010)
Setting maximal mount count to 8
Setting interval between checks to 1296000 seconds
```

The next tune2fs command is similar but works on a different partition and sets the current mount count to 4. When you do not specify a current mount count, it is set to zero:

```
$ sudo tune2fs -c 8 -i 15 -C 4 /dev/sda6
tune2fs 1.41.11 (14-Mar-2010)
Setting maximal mount count to 8
Setting current mount count to 4
Setting interval between checks to 1296000 seconds
```

The -l option lists a variety of information about the partition. You can combine this option with others. A maximum mount count of -1 or 0 means fsck and the kernel will ignore the mount count information.

```
$ sudo tune2fs -l /dev/sda6
tune2fs 1.41.11 (14-Mar-2010)
Filesystem volume name:   <none>
Last mounted on:              /home
Filesystem UUID:      eladaf6b-39e8-4658-82ac-6f75ecdb82c4
Filesystem magic number:      0xef53
Filesystem revision #:       1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent flex_bg sparse_super large_file huge_file uninit_bg dir_nlink extra_isize
Filesystem flags:      signed_directory_hash
Default mount options:       (none)
Filesystem state:      clean
Errors behavior:     Continue
Filesystem OS type:     Linux
Inode count:      125376
Block count:      5012992
Reserved block count: 250649
Free blocks:      4278628
Free inodes:      1110959
First block:      0
Block size:      4096
Fragment size:      4096
...
```

> 1. For systems whose purpose in life is to run continuously, this kind of scheduling does not work. You must develop a schedule that is not based on system reboots but rather on a clock. Each filesystem must be unmounted periodically, checked with fsck (preceding section), and then remounted.
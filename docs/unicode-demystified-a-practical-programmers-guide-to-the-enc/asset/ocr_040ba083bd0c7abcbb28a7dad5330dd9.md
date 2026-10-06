partition, the more time it takes to check it, assuming a nonjournaling filesystem. These checks are frequently unnecessary. The tune2fs utility helps you to find a happy medium between checking filesystems each time you reboot the system and never checking them. It does this by scheduling when fsck checks a filesystem (these checks occur only when the system is booted).²25 You can use two scheduling patterns: time elapsed since the last check and number of mounts since the last check. The following command causes /dev/hda6 to be checked when fsck runs eight times or after 15 days have elapsed since its last check, which happens first:

```
# tune2fs -c 8 -i 15 /dev/hda6
tune2fs 1.27, (8-Mar-2002)
Setting maximal mount count to 8
Setting interval between check 1296000 seconds
```

The next tune2fs command is similar except that it works on a different partition and sets the current mount count to 4. When you do not specify a current mount count, in the previous example, it is assumed to be:

```
# tune2fs -c 8 -i 15 -C 4 /dev/hda10
tune2fs 1.27, (8-Mar-2002)
Setting maximal mount count to 4
Setting current mount count to 4
Setting interval between check 1296000 seconds
```

The -l option displays a list of information about the partition. You can combine this option with others. Below the Maximum mount count is -1, which means the mount count information is ignored by fsck and the kernel. A mount count of 0 works the same way:

```
# tune2fs -l /dev/hda5
tune2fs 1.27, (8-Mar-2002)
Filesystem volume name: /free
Last mounted: <not available>
Filesystem UUID: f59d69a8-a419-11d4-944c-e771d63cd639
Filesystem magic number: 0EF53
Filesystem revision: 1 (dynamic)
Filesystem features: has_journal filetype needs_recovery sparse_super
Filesystem state: clean
Errors behavior: Continue
Filesystem OS type: Linux
Inode count: 513024
Block count: 1024135
```

2. For systems whose purpose in life is to run continuously, this kind of scheduling does not work. You must come up with a schedule that is not based on system reboots but rather on a clock. Each filesystem must be mounted periodically, checked with fsck (preceding section), and remounted.
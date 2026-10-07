# v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

If you run the fls command with the -o option to specify the file system, then by default it will run on the file system's root directory. This is inode 2 on an EXT file system and MFT entry 5 on an NTFS file system.

In other words, an EXT file system, running:

```
barry@forensic1:-~/abled$ fls -o 10260 able2.dd
```

And...

```
barry@forensic1:-~/abled$ fls -o 10260 able2.dd 2
```

...will result in the same output. In the second command, the 2 passed at the end of the command means "root directory"(for EXT), which is the default in the first command.

So, in the following command, we run fls and only pass -o 10260. This results in a listing of the contents of the root directory:

```
barry@forensic1:-~/abled$ fls -o 10260 able2.dd
d/d 11: lost+found
d/d 3681: boot
d/d 7361: usr
d/d 3682: proc
d/d 7362: var
d/d 5521: tmp
d/d 7363: dev
d/d 9201: etc
d/d 1843: bin
d/d 1844: home
d/d 7368: lib
d/d 7369: mnt
d/d 7370: opt
d/d 1848: root
d/d 1849: sbin
r/r 1842: .bash_history
d/d 11105: .001
d/d 12881: $OrphanFiles
```

There are several points we want to take note of before we continue. Let's take a few lines of output and describe what the tool is using us. Have a look at the last three lines of the above fls command.

214
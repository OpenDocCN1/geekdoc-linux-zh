# F.3.7 Why does Linux only see part of my RAM?

There are a couple things that could be wrong. On some 386's, you need to compile your kernel with “Limit memory to 16M?” enabled. Some AMI BIOS motherboards have a memory option to split memory into two segments. I'm not sure what the option is called, but it has something to do with “linear”. You'll find it in your BIOS setup. You may need to specify the amount of memory to the kernel at boot time from lilo. To try this, type: linux mem=32M at the lilo prompt. If that works, you can add that line to the append in your /etc/lilo.conf and rerun lilo. The example from above would be:

```
append = "mem=32M"
```

Don't forget to run 'lilo' after editing the file.

# F.3.8 How do I install to my DOS partition?

You can't. None of the current Red Hat releases support UMSDOS installs. If you have one drive that has one big DOS partition with free space you want to use, you have two options. One is to backup all your DOS data somehow and then repartition the drive into smaller partitions and then restore the DOS data back to a DOS partition. You then have a free partition for linux. The second choice is to use fips. fips is a program that will let you change your partition size of a DOS partition without harming the data on it. It is STRONGLY suggested that you backup your data before using fips. Red Hat Software makes no warranties or claims as to the suitability of using fips for this purpose nor can we guarantee that data will remain unharmed. I haven't heard of anyone having a bad experience with fips, but I won't guarantee it either.

# F.3.9 How do I use the NYS/NIS system that comes with RedHat?

Please see the NYS-Tips. You can find it at http://www.redhat.com/.
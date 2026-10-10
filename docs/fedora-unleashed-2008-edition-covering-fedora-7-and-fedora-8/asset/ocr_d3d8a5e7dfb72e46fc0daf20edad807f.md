The format for the command is the following:

/sbin/mkinitrd fileName kernel_version

where **fileName** is the name of the image file you want created.

mkinitrd looks at /etc/fstab, /etc/modprobe.conf, and /etc/raidtab to obtain the information it needs to determine which modules should be loaded during boot. For our personal systems, we use the following:

# mkinitrd initrd-2.6.7-1.img 2.6.7-1

# ## When Something Goes Wrong

Several things might go wrong during a kernel compile and installation, and several clues will point to the true problem. You will see error messages printed to the screen, and some error messages will be printed to the file /var/log/messages, which can be examined with a text editor. If you have followed our directions for patching the kernel, you will have to examine a special error log as well. Do not worry about errors because many problems are easily fixed with some research on your part. Some errors may be unfixable, however, depending on your skill level and the availability of technical information.

# ### Errors During Compile

Although it is rare that the kernel will not compile, there is always a chance that something has slipped though the regression testing. Let's take a look at an example of a problem that might crop up during the compile.

It is possible that the kernel compile will crash and not complete successfully, especially if you attempt to use experimental patches, add untested features, or build newer and perhaps unstable modules on an older system. For examples, the kernel compile will fail on an older-stock Red Hat 7.2 installation using the 2.4.9 kernel when the NTFS file system is selected, either as a loadable module or inline, as shown here:

```
```
gcc -O_KERNEL_ -I/usr/src/kernels/linux-2.4.9/include -Wall -Wstrict-prototypes
-Wno-trigraphs -O2 -fomit-frame-pointer -fno-strict-aliasing -fno-common
-pipe -mprefer-scaled -stack-boundary=2 -march=athlon -DMODULE -DMODVERSIONS
-include /usr/src/kernels/linux-2.4.9/include/linux/modversions.h
-DNTFS_VERSION='\"1.16\"' Â)
-> .c o unistr.o unistr.c
unistr.c: In function 'ntfs_collate_names' :
unistr.c:99: warning: implicit declaration of function 'min'
unistr.c:99: parse error before 'unsigned'
unistr.c:99: parse error before ' )'
unistr.c:97: warning: 'c1' might be used uninitialized in this function
unistr.c: At top level:
unistr.c:118: parse error before 'if'
```
```

![](bbox=[0.92, 0.55, 0.98, 0.62])
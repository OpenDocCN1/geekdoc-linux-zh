# ## Creating Swap Space

Some partitions don't hold files. Most notably, Linux can use a *swap partition*, which is a partition that Linux treats as an extension of memory. (Linux can also use a *swap file*, which is a file that works in the same way. Both are examples of *swap space*.) Linux uses the MBR partition type code of 0x82 to identify swap space, but as with other partitions, this code is mostly a convenience to keep other OSs from trying to access Linux swap partitions; Linux uses `/etc/fstab` to define which partitions to use as swap space, as described in Chapter 4, “Managing Files.”

![](bbox=[0.15, 0.3, 0.24, 0.36])

> Solaris for x86 also uses an MBR partition type code of 0x82, but in Solaris, this code refers to a Solaris partition. If you dual-boot between Solaris and Linux, this double meaning of the 0x82 partition type code can cause confusion. This is particularly true when installing the OSs. You may need to use Linux's fdisk to temporarily change the partition type codes to keep Linux from trying to use a Solaris partition as swap space or to keep Solaris from trying to interpret Linux swap space as a data partition.

Although swap space doesn't hold a filesystem *per se* and isn't mounted in the way that filesystem partitions are mounted, swap space does require preparation similar to that for creation of a filesystem. This task is accomplished with the **mkswap** command, which you can generally use by passing it nothing but the device identifier:

```
# mkswap /dev/hda7
```

This example turns `/dev/hda7` into swap space. To use the swap space, you must activate it with the **swapon** command:

```
# swapon /dev/hda7
```

To permanently activate swap space, you must create an entry for it in `/etc/fstab`, as described in Chapter 4.

# # Maintaining Filesystem Health

Filesystems can become “sick” in a variety of ways. They can become overloaded with too much data, they can be tuned inappropriately for your system, or they can become corrupted because of buggy drivers, buggy utilities, or hardware errors. Fortunately, Linux provides a variety of utilities that can help you keep an eye on the status of your filesystems, tune their performance, and fix them.
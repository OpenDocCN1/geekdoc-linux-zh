# **Background Material**

You can specify different-sized chunks for input and output with `ibs=` and `obs=`, respectively.

The `count=32k` tells `dd` to read 32KB (that is, 32 × 1024 = 32,768) blocks. The combination of block size and count yields 32 × 1024 × 1024 bytes, or 32MB.

Because sensitive information may be placed in a swap file when a process is swapped out, you should make sure the swap file is owned by root and is not readable by other users. Do this as follows:

```
`# chown root:root /swapfile`
`# chmod go-rwx /swapfile`
```

# ## Formattting a Swap Area

Before you can use a swap file or partition, you must format it. This needs to be done only once, immediately after the swap file or partition is created.

To format a swap partition, use the `mkswap` command:

```
`# mkswap /swapfile; sync`
`# mkswap -C /dev/hdc3`
```

In the first example, we use `mkswap` on a swap file. Because a swap file is a normal file in the file system, we use the `sync` command to flush the output to disk. This makes sure that the formatting information is really written to the disk and not just buffered in memory.

In the second, we use it on a swap partition. For swap partitions, supply the name of the device file representing the partition. Also, for the partition, we use the `-C` option, which tells `mkswap` to check for bad disk blocks. Always use `-C` when formatting a swap partition; never use it when formatting a swap file.

# **Background Material**

The method of keeping track of swap space changed between kernel versions 2.0 and 2.2. The "old style" allows an area of swap space to be at most about 128MB, whereas the "new style" allows it to be about 2GB. `mkswap` automatically chooses the appropriate style. (Don't make more swap space than about twice your physical RAM—if you really start using that much virtual memory, the disk paging will slow your system to a crawl.)
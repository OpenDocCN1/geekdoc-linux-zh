To mount a vnode-backed memory disk, use the `-F` flag and the path to the image file.

```
`# mdmfs -F diskimage.file md /mnt`
```

The `md` entry we’ve been using all along here means, “I don’t care what device name I get; just give me the next free one.” You can also specify a particular device name if you like. Here, I declare I want disk device `/dev/md9`:

```
`# mdmfs -F diskimage.file md9 /mnt`
```

# ## Memory Disk Headaches

Traditional swap-backed memory disks never returned used memory to the system. Once you wrote to a memory disk, that memory was used up. If you needed a larger memory disk, you had to permanently allocate memory for it. This was one reason FreeBSD included tmpfs(5).

If the filesystem on the memory disk supports TRIM, however, FreeBSD now returns unused memory to the system. TRIM is not an acronym but rather a protocol for telling a disk which sectors are no longer in use. UFS, the default memory disk format, supports TRIM. Enable TRIM in mdmfs with the `-t` flag. If you’re using a different filesystem on a memory disk, though, be sure it’s strictly temporary.

To free the memory from a memory disk, shut down the memory disk.

# ## Memory Disk Shutdown

To remove a memory disk, you must unmount the partition and destroy the disk device. Destroying the disk device frees the memory used by the device, which is useful when your system is heavily loaded. To find the disk device, run mount(8) and find your memory disk partition. Somewhere in the output, you’ll find a line like this:

```
`/dev/md41 on /mnt (ufs, local, soft-updates)`
```
# 64-bit Files in Solaris

If the compilation environment can be set for either small files or large files, it is safest to place #ifdef around the format string, such as:

```
off_t offset;
#if FILE_OFFSET_BITS - 0 == 64
printf("%7ld", offset);
else
printf("%7d", offset);
#endif
```

You can find more information on the transitional and large-file interfaces in the system manual pages, under interface64(5), lf64(5), and lfcompile(64).

Note that the transitional interfaces exist for 32-bit Solaris. Beginning with 64-bit Solaris, the file interfaces use the 64-bit data types for file offsets.

# 11.6.4 File System Support for Large Files

Starting with Solaris 2.6, large-file support was added to the UFS, CACHEFS, and NFSV3 file systems. Each of these file systems can contain files larger than 2 gigabytes and can support to seek within the large offsets.

The UFS provides a mount option to control how it handles large files. By default, it supports large files. Support for large files was also added to swapfs, which allows us to add swap devices and swap files of sizes up to 1 terabyte. Note that the tmpfs in Solaris 2.6 has a maximum file size of 2 gigabytes. The maximum file size is unlimited with Solaris 7 in 64-bit mode.
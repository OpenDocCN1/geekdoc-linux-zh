Note that this example shows that the floppy has only 1.3MB available! What happened to the extra 5 percent? Linux automatically reserves extra room on every volume for the root operator. This means that there is potentially 300MB of extra storage available on a 6GB hard drive! To make as much room as possible available on a volume, such as a floppy or hard drive, use the `mkexts` command's `-m` option with a value of 0 to specify no reserve room:

```
`$ mkexts -m 0 /dev/fd0`
```

After formatting and mounting, the `df` command reports:

```
```
$ df /mnt/floppy
Filesystem     Size  Used Avail Use% Mounted on
/dev/fd0       1.4M   13k  1.4M   1% /mnt/floppy
```
```

As you can see, the entire floppy is now available. This can make a big difference, especially if you're trying to squeeze out as much room as possible on the floppy, and it makes a very big difference if you're installing a new hard drive for Linux! (Note that you can also *increase* the amount of room to reserve for the root operator, but this wouldn't make much sense.)

# Macintosh HFS Support

File utilities for other operating systems, such as the Macintosh, are also found with most Linux distributions. One package, `hfsutls`, includes a number of programs that you can use much like those included in the `mtools` package. For example, to create a 1.44MB Macintosh HFS diskette, use the `hformat` command like this:

```
```
$ hformat /dev/fd0
Volume name is "Untitled"
Volume was created on Mon Feb 28 16:05:57 2000
Volume was last modified on Mon Feb 28 16:05:57 2000
Volume has 1448960 bytes free
```
```

You can then mount the new Macintosh floppy like this:

```
`$ mount -t hfs /dev/fd0 /mnt/floppy`
```

Alternatively, you can use the `hmount` command like this:

```
`$ hmount /dev/fd0`
```

You would then use the various `hfsutls`—such as `hcopy`, `hdel`, or `hls`—to copy, delete, or list files on the floppy. Although the Apple iBook does not come with an
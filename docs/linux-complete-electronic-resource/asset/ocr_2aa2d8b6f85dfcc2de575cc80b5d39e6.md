| F | Format the partition as FAT32 (experimental). |
| :-- | :--- |
| I | Sets the fsVersion id when formatting a FAT32 drive. In order to find this out, run minifo on an existing FAT32 drive, and mail me about it, so I can include the correct value in future versions of mttools. |
| c | Sets the size of a cluster (in sectors). If this cluster size would generate a FAT that is too big for its number of bits, mtools automatically increases the cluster size, until the FAT is small enough. |
| r | Sets the size of the root directory (in sectors). Only applicable to 12 and 16 bit FATs. |

To format a diskette at a density other than the default, you must supply (at least) those command line parameters that are different from the default.

**Mformat** returns 0 on success or 1 on failure.

It doesn’t record bad block information to the Fat, use mkmmanifest for that.

# MKMANIFEST

The **mkmanifest** command is used to create a shell script (packing list) to restore Unix filenames. Its syntax is:

```
``` 
mkmanifest [ files ] 
```
```

**Mkmanifest** creates a shell script that aids in the restoration of Unix filenames that got clobbered by the MS-DOS filename restrictions. MS-DOS filenames are restricted to 8 character names, 3 character extensions, upper case only, no device names, and no illegal characters.

The mkmanifest program is compatible with the methods used in **pcomm**, **arc**, and **mtools** to change perfectly good Unix filenames to fit the MS-DOS restrictions. This command is only useful if the target system which will read the diskette cannot handle vfat long names.

# EXAMPLE

You want to copy the following Unix files to a MS-DOS diskette (using the mcopy command).

+   - very\_long\_name
+   - 2.many.dots
+   - illegal:
+   - good.c
+   - prn.dev
+   - Capital
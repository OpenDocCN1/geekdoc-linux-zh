+   2. Run the `rpm -ivh e2fsprogs-version.src.rpm` command to extract the source into a `/usr/src/redhat/SOURCES/` directory. The source RPM drops a `e2fsprogs-version.tar.gz` file, which needs to be extracted with the `tar xzvf e2fsprogs-version.tar.gz` command. This creates a subdirectory called `e2fsprogs-version`.
+   
+   3. Change to the new subdirectory `e2fsprogs-version`.
+   
+   4. Run `mkdir build` to create a new subdirectory and then change to that subdirectory.
+   
+   5. Run `.../configure` script to configure the source tree. Then run the `make` utility to create the binaries. Then run `make check` to ensure that everything is built correctly. Finally, run the `make install` command to install the binaries.

After you have installed the e2fsprogs utilities you can start using them as discussed in the following section.

# ### Using the tune2fs utility for file-system tuning

You can use the `tune2fs` utility to tune various aspects of an ext2 file system. However, you should never apply the tune2f utilities on a mounted ext2 and always back up your data whenever you are modifying anything belonging to a file system. In this section, I discuss how to use the `tune2fs` utility (which is part of the e2fsprogs package) to tune an unmounted ext2 file system called `/dev/hda7`. If you use one or more of the settings discussed below, don't forget to change the partition name (`/dev/hda7`) to the appropriate name. First, run the following command to determine what `tune2fs` shows as the current settings for the unmounted `/dev/hda7`:

```
`/sbin/tune2fs -l /dev/hda7`
```

The output should be something similar to the following:

```
```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:              <not available>
Filesystem UUID:     5d06c65b-dd11-4df4-9230-a10f2da783f8
Filesystem magic number:      0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:    filetype sparse_super
Filesystem state:    clean
Errors behavior:    Continue
Filesystem OS type:    Linux
Inode count:    1684480
Block count:    13470471
Reserved block count:  673523
Free blocks:    13225778
Free inodes:    1674469
First block:    1
Block size:    1024
Fragment size:    1024
```
```
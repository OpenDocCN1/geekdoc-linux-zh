# Installing *e2fsprogs*

To tune the ext2 file system, you need to install the *e2fsprogs* utility package as follows:

+   1. Download the `e2fsprogs-version.src.rpm` (replace `version` with the latest version number) source distribution from `www.rpmfind.net`. I downloaded the `e2fsprogs-1.19-0.src.rpm` package. You can also get the source from the *e2fsprogs* project site at `http://e2fsprogs.sourceforge.net`.
+   2. Run the `rpm -ivh e2fsprogs-version.src.rpm` command to extract the source into `~/usr/src/redhat/SOURCES/` directory. The source RPM drops a `e2fsprogs-version.tar.gz` file that needs to be extracted using the `tar xvzf e2fsprogs-version.tar.gz` command. This creates a subdirectory called `e2fsprogs-version`.
+   3. Change to the new subdirectory.
+   4. Run `mkdir build` to create a new subdirectory and then change to that directory.
+   5. Run `../configure` script to configure the source tree.
+   6. Run the `make` utility to create the binaries.
+   7. Run the `make check` command to ensure that everything is built correctly.
+   8. Run the `make install` command to install the binaries.

After you have installed the *e2fsprogs* utilities you can start using them as discussed in the following sections.

# Tuning your file system with `tune2fs`

You can use the `tune2fs` utility to tune various aspects of an ext2 file system.

> > You should never apply the ext2 utilities on a mounted ext2 and you should always back up your data whenever you are modifying anything belonging to a file system.

The following section discusses how to use the `tune2fs` utility (part of the *e2fsprogs* package) to tune an unmounted ext2 file system called `/dev/hda7`. If you one or more of the settings discussed below, don’t forget to change the partition name (`/dev/hda7`) to the appropriate name. First, let’s look at what `tune2fs` shows as the current settings for the unmounted `/dev/hda7` by running the following command:

```
/sbin/tune2fs -l /dev/hda7
```

The output should be similar to this:

```
tune2fs 1.19, 13-Jul-2000 for EXT2 FS 0.5b, 95/08/09
Filesystem volume name:   <none>
Last mounted on:          <not available>
```
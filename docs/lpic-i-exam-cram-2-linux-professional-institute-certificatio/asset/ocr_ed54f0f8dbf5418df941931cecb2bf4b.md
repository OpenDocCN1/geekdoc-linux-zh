For example, consider the `/test` directory again, with its structure similar to the following:

```
-- dir1
    |-- file1
    `-- subdir1
-- dir2
```

If you were a Windows administrator, it would make sense to run the following command to move `dir1` to `dir2`:

```
mv dir1 dir2
```

If you run the `tree` command, you see the following output:

```
-- dir2
    -- dir1
        |-- file1
        `-- subdir1
```

To properly move the contents of the source `dir1` to the target `dir2`, you don't need to use the nonexistent `-r` option (exam trick). You can just use a forward slash and an asterisk, like this:

```
mv dir1/* dir2
```

If you run the `tree` command, you see the following output:

```
-- dir1
-- dir2
    |-- file1
    `-- subdir1
```

Finally, when you're using the `mv` command to move directories around on the system, the exam might say you are in a given directory and want to move the *contents* of `/dir1` to the current directory. You'll then be asked the shortest way to accomplish this. This answer is

```
mv /dir1/* .
```

# ## Transforming Data Formats

The `dd` command is useful for a variety of tasks, not the least of which is creating ISO files from CD-ROMs you want to copy. The two main formats `dd` interacts with are the raw device file and the full path of a file or object on the system.

For example, when creating a new boot disk, the `.img` binary file is read block by block from the CD-ROM (as a file) and written to the floppy raw device as a set of blocks:

```
dd if=/mnt/cdrom/images/boot.img of=/dev/fd0
```

Creating an image of a floppy involves reading the raw floppy device block by block and creating a file on the file system that contains all those blocks:

```
dd if=/dev/fd0 of=/root/floppy.img
```
# # Checking System Space

Running out of disk space on your computer is not a happy situation. Using tools that come with Red Hat Linux, you can keep track of how much disk space has been used on your computer, and you can keep an eye on users who consume a lot of disk space.

# ## Displaying system space with df

You can display the space available in your file systems using the `df` command. To see the space available on all of the mounted file systems on your Linux computer, type `df` with no options:

```
```
$ df
Filesystem     1k-blocks    Used Available Use% Mounted on
/dev/hda3      30645460  2958356 26130408  11% /
/dev/hda2         46668   8340    35919  19% /boot
/dev/fd0            1412     13     1327   1% /mnt/floppy
```
```

The output here shows the space available on the hard disk partition mounted on the root partition (`/dev/hda1`), `/boot` partition (`/dev/hda2`), and the floppy disk mounted on the `/mnt/floppy` directory (`/dev/fd0`). Disk space is shown in 1K blocks. To produce output in a more human-readable form, use the `-h` option as follows:

```
```
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/hda3       29G  2.9G  24G   11% /
/dev/hda2       46M  8.2M  25M   19% /boot
/dev/fd0        1.4M  13k  1.2M   1% /mnt/floppy
```
```

With the `df` `-h` option, output appears in a friendlier megabyte or gigabyte listing. Other options with `df` let you:

+   - Print only file systems of a particular type (`-t type`)

+   - Exclude file systems of a particular type (`-x type`)

+   - Include file systems that have no space, such as `/proc` and `/dev/pts` (`-a`)

+   - List only available and used inodes (`-i`)

+   - Display disk space in certain block sizes (`--block-size=#`)

# ## Checking disk usage with du

To find out how much space is being consumed by a particular directory (and its subdirectories), you can use the `du` command. With no options, `du` lists all directories below the current directory, along with the space consumed by each directory. At the end, `du` produces total disk space used within that directory structure.

# The Linux Cookbook: Tips and Techniques for Everyday Use:

```
$ ls -l /usr/doc/bash RET
total 72
-rw-r--r--  1 root    root     13744 Oct 19 22:57 CHANGES.gz
-rw-r--r--  1 root    root      1816 Oct 19 22:57 COMPAT.gz
-rw-r--r--  1 root    root     16398 Oct 19 22:57 FAQ.gz
-rw-r--r--  1 root    root      2928 Oct 19 22:57 INTRO.gz
-rw-r--r--  1 root    root      4751 Oct 19 22:57 NEWS.gz
-rw-r--r--  1 root    root      1588 Oct 19 22:57 POSIX.NOTES.gz
-rw-r--r--  1 root    root      2718 Oct 19 22:57 README.Debian.gz
-rw-r--r--  1 root    root     19596 Oct 19 22:57 changelog.gz
-rw-r--r--  1 root    root      1446 Oct 19 22:57 copyright
 drwxr-xr-x  9 root    root      1024 Jul 25  1997 examples
$
```

This command outputs a verbose listing of the files in `/usr/doc/bash`. The first line of output gives the total amount of disk space, in 1024-byte blocks, that the files take up (in this example, 72). Each subsequent line displays several columns of information about one file.

The first column displays the file’s type and permissions. The first character in this column specifies the file type; the hyphen (`-`) is the default and means that the file is a regular file. Directories are denoted by `d`, and symbolic links (see section [Giving a File More than One Name](#)) are denoted by `l`. The remaining nine characters of the first column show the file permissions (see section [Controlling Access to Files](#)). The second column lists the number of hard links to the file. The third and fourth columns give the names of the user and group that the file belongs to. The fifth column gives the size of the file in bytes, the sixth column gives the date and time of last modification, and the last column gives the file name.

[<] [>]   [<<] [Up] [>>]   [Top] [Contents] [Index] [?]

## 6.3.2 Listing Directories Recursively

Use the `-R` option to list a directory recursively, which outputs a listing of that directory and all of its subdirectories.

- To output a recursive directory listing of the current directory, type:

```
$ ls -R RET
play    work

play:
notes

work:
notes
$
```

In this example, the current working directory contains two subdirectories, `work` and `play`, and no other files. Each subdirectory contains a file called `notes`.

- To list all of the files on the system, type:

```
$ ls -R / RET
```

This command recursively lists the contents of the root directory, `/`, and all of its subdirectories. It is common to combine this with the attribute option, `-l`, to output a verbose listing of all the files on the system:

```
$ ls -lR / RET
```

*NOTE:* You can't list the contents of some directories on the system if you don't have permission to do so (see section Controlling Access to Files).

## 6.3.3 Listing Newest Files First

Use the `-t` option with ls to sort a directory listing so that the newest files are listed first.

- To list all of the files in the `/usr/tmp` directory sorted with newest first, type:

```
$ ls -t /usr/tmp RET
```

## 6.3.4 Listing Hidden Files

By default, ls does not output files that begin with a period character (`.`). To reduce clutter, many applications "hide" configuration files in your home directory by giving them names that begin with a period; these are called dot files, or sometimes "hidden" files. As mentioned earlier, every directory has two special dot files: `..`, the parent directory, and `.`, the directory itself.

To list all contents of a directory, including these dot files, use the `-a` option.

- To list all files in the current directory, type:

```
$ ls -a RET
```

Use the `-A` option to list almost all files in the directory: it lists all files, including dot files, with the exception of `.` and `..`.

- To list all files in the current directory except for `.` and `..`, type:

```
$ ls -A RET
```

## 6.3.5 Listing Directories in Color

Use ls with the `--color` option to list the directory contents in color; files appear in different colors depending on their content. Some of the default color settings include displaying directory names in blue, text files in white, executable files in green, and links in turquoise.

- To list the files in the root directory in color, type:

```
$ ls --color /
System.map  etc        man        usr
System.old  floppy     mnt        var
bin         home       proc       vmlinuz
boot        initrd     root       vmlinuz.old
cdrom       lib        sbin
dev         lost+found tmp
$
```

NOTE: It's common practice to create a command alias that substitutes `ls --color` for `ls`, so that typing just ls outputs a color listing. To learn more about making aliases, see Making a Command Alias.

## 6.3.6 Listing Directory Tree Graphs

```
@sf(Debian): `tree`
@sf(WWW): http://mama.indstate.edu/linux/tree/
```

Use tree to output an ASCII tree graph of a given directory tree.

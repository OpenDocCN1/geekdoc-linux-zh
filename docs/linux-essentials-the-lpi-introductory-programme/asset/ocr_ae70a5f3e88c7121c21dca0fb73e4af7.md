You can unpack the data using the `-x` option:

```
```text
$ tar -xf data.tar
```
```

In this case tar produces no output on the terminal at all—you have to give the `-v` option again:

```
```text
$ tar -xvf data.tar
data1
data10
data2
```
```

If the archive contains a directory hierarchy, this is faithfully reconstructed in the current directory. (You will remember that tar makes relative path names from all absolute ones.) You can unpack the archive relative to any directory—it always keeps its structure.

You can also give file or directory names on unpacking. In this case only the files or directories in question will be unpacked. However, you need to take care to match the names in the archive exactly:

```
```bash
$ tar -cf data.tar ./data
$ tar -tvf data.tar
drwxr-xr-x joe/joe    0 2009-01-27 12:04 ./data/
-rw-r--r-- joe/joe    7 2009-01-27 12:04 ./data/data2
$ mkdir data-new
$ cd data-new
$ tar -xvf ../data.tar data/data2
                                  . / missing
tar: data/data2: Not found in archive
tar: Error exit delayed from previous errors
```
```

# Exercises

+   **11.3** [2] Store a list of the files in your home directory in a file called content. Create a tar archive from that file. Compare the original file and the archive. What do you notice?

+   **11.4** [2] Create three or four empty files and add them to the archive you just created.

+   **11.5** [2] Remove the original files and then unpack the content of the tar archive.

+   **11.6** [2] Why does GNU tar prophylactically remove the / at the beginning of the path name, if the name of a file or directory to be archived is given as an absolute path name? (Hint: Consider the

```
```text
# tar -cvf /tmp/etc-backup.tar /etc
```
```

command and imagine what will happen if etc-backup.tar (a) contains absolute path names, and (b) is transferred to another computer and unpacked there.)
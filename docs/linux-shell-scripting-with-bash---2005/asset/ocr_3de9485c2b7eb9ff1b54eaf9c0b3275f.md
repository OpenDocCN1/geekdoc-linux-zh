The **Linux tar** (*tape archive*) command is the most commonly used archiving com-
mand, and it automatically compresses while archiving when the right command-line
options are used. Although the command was originally used to collect files for storage
on tape drives, it can also create disk files.

Originally, the **tar** command didn't use command-line switches: A series of single
characters were used. The Linux version supports command-line switches as well as the
older single character syntax for backward compatibility.

To use **tar** on files, the `--file` (*F* (or *-f*) switch indicates the filename to act on. At
least one action switch must be specified to indicate what **tar** will do with the file.
Remote files can be specified with a preceding hostname and a colon.

The `--create` (*-c*) switch creates a new tar file.

```
$ ls -1 orders.txt
-rw-rw-r--  1 kburcht  kburcht     592 May 11 14:45 orders.txt
$ tar --create --file orders.tar orders.txt
$ ls -1 orders.tar
-rw-rw-r--  1 kburcht  kburcht   10240 Oct  3 12:06 orders.tar
```

The archive file is significantly larger than the original file. To apply compression,
choose the type of compression using `--bzip` (or *-I*), `--gzip` (or *-z*), `--compress` (or *-Z*),
or `--use-compress-program` to specify a particular compression program.

```
$ tar --create --file orders.tbz --bzip orders.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     421 Oct  3 12:12 orders.tbz
$ tar --create --file orders.tgz --gzip orders.txt
$ ls -1 orders.tgz
-rw-rw-r--  1 kburcht  kburcht     430 Oct  3 12:11 orders.tgz
```

More than one file can be archived at once.

```
$ tar --create --file orders.tbz --bzip orders.txt orders2.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     502 Oct  3 12:14 orders.tbz
```

The new archive overwrites an existing one.

To restore the original files, use the `--extract` switch. Use `--verbose` to see the file-
names. **tar** cannot auto-detect the compression format; you must specify the proper
compression switch to avoid an error.

```
$ tar --extract --file orders.tbz
tar: 502 garbage bytes ignored at end of archive
tar: Error exit delayed from previous errors
$ tar --extract --bzip --file orders.tbz
$ tar --extract --verbose --bzip --file orders.tbz
orders.txt
orders2.txt
```
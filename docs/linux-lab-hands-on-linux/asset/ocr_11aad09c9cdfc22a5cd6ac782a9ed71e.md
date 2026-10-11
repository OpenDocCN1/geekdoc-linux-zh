```
cpio flags [options]
```

Following is the syntax for creating the cpio file:

```
find (source file name) | cpio - (Options) > (target file name)
```

For example.

```
find filel | cpio -o > file1_back.cpio
```

Following syntax is used for extracting the cpio file:

```
cat <source file name> | cpio - (Options)
```

For example.

```
cat filel_back.cpio | cpio -idvm
```

# Dump and Restore

The dump and restore commands are two different programs that are included in the dump package. Following is the syntax of dump command, which is used to backup the directory into a file:

```
dump - <dump level> - <options> <destination name> <source name>
```

For example.

```
dump -0 -f /home_dumps/mydumps /home
```

![](bbox=[0.34, 0.7, 0.71, 0.81])

The restore command is used to view and restore the dump file. Following is the syntax of the restore command used to view and restore the dump files:
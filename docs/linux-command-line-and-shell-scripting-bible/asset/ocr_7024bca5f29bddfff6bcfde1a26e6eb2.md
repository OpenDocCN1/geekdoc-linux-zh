# Archiving data

While the zip command works for compressing and archiving data into a single file, it's not the standard utility used in the Unix and Linux worlds. By far the most popular archiving tool used in Unix and Linux is the tar command.

The tar command was originally used to write files to a tape device for archiving. However, it can also write the output to a file, which has become a popular way to archive data in Linux.

The format of the tar command is:

```
tar function [options] object1 object2 ...
```

The function parameter defines what the tar command should do, as shown in Table 4-9.

Each function uses options to define a specific behavior for the tar archive file. Table 4-10 lists the common options that you can use with the tar command.

These options are usually combined to create the following scenarios:

```
tar -cvf test.tar test/ test2/
```

| Function | Long name | Description |
|---|---|---|
| -A | --concatenate | Append an existing tar archive file to another existing tar archive file. |
| -c | --create | Create a new tar archive file. |
| -d | --diff | Check the differences between a tar archive file and the filesystem. |
| | --delete | Delete from an existing tar archive file. |
| -r | --append | Append files to the end of an existing archive file. |
| -t | --list | List the contents of an existing archive file. |
| -u | --update | Append files to an existing archive file that are newer than a file with the same name in the existing archive. |
| -x | --extract | Extract files from an existing archive file. |
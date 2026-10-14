
## Tests

On most active user accounts, this will produce a large list. Because the list is sent to standard output, we can pipe the list into other programs. Let’s use wc to count the number of files.

```
[me@linuxbox ~]$ find ~ | wc -l
47068
```

Wow, we’ve been busy! The beauty of find is that it can be used to identify files that meet specific criteria. It does this through the (slightly strange) application of options, tests, and actions. We’ll look at the tests first.

Let’s say we want a list of directories from our search. To do this, we could add the following test:

```
[me@linuxbox ~]$ find ~ -type d | wc -l
1695
```

Adding the test -type d limited the search to directories. Conversely, we could have limited the search to regular files with this test:

```
[me@linuxbox ~]$ find ~ -type f | wc -l
38737
```

Table 17-1 lists the common file type tests supported by find.

### Table 17-1: find File Types

| File type | Description |
|---|---|
| b | Block special device file |
| c | Character special device file |
| d | Directory |
| f | Regular file |
| l | Symbolic link |

We can also search by file size and filename by adding some additional tests. Let’s look for all the regular files that match the wildcard pattern *.JPG and are larger than one megabyte.

```
[me@linuxbox ~]$ find ~ -type f -name "*.JPG" -size +1M | wc -l
840
```

In this example, we add the -name test followed by the wildcard pattern. Notice how we enclose it in quotes to prevent pathname expansion by the shell. Next, we add the -size test followed by the string +1M. The leading plus sign indicates that we are looking for files larger than the specified number. A leading minus sign would change the meaning of the string to be smaller than the specified number. Using no sign means “match the value exactly.” The trailing letter M indicates that the unit of measurement is megabytes. Table 17-2 lists the characters that can be used to specify units.

### Table 17-2: find Size Units

| Character | Unit |
|---|---|
| b | 512-byte blocks. This is the default if no unit is specified. |
| c | Bytes. |
| w | 2-byte words. |
| k | Kilobytes (units of 1,024 bytes). |
| M | Megabytes (units of 1,048,576 bytes). |
| G | Gigabytes (units of 1,073,741,824 bytes). |

find supports a large number of tests. Table 17-3 provides a rundown of the common ones. Note that in cases where a numeric argument is required, the same + and - notation discussed previously can be applied.

### Table 17-3: find Tests

| Test | Description |
|---|---|
| `-cmin n` | Match files or directories whose content or attributes were last modified exactly *n* minutes ago. To specify less than *n* minutes ago, use `-n`, and to specify more than *n* minutes ago, use `+n`. |
| `-cnewer file` | Match files or directories whose contents or attributes were last modified more recently than those of *file*. |
| `-ctime n` | Match files or directories whose contents or attributes were last modified *n*24 hours ago. |
| `-empty` | Match empty files and directories. |
| `-group name` | Match files or directories belonging to group *name*. *name* may be expressed either as a group name or as a numeric group ID. |
| `-iname pattern` | Like the `-name` test but case-insensitive. |
| `-inum n` | Match files with inode number *n*. This is helpful for finding all the hard links to a particular inode. |
| `-mmin n` | Match files or directories whose contents were last modified *n* minutes ago. |
| `-mtime n` | Match files or directories whose contents were last modified *n*24 hours ago. |
| `-name pattern` | Match files and directories with the specified wildcard *pattern*. |
| `-newer file` | Match files and directories whose contents were modified more recently than the specified *file*. This is useful when writing shell scripts that perform file backups. Each time you make a backup, update a file (such as a log) and then use find to determine which files have changed since the last update. |
| `-nouser` | Match files and directories that do not belong to a valid user. This can be used to find files belonging to deleted accounts or to detect activity by attackers. |
| `-nogroup` | Match files and directories that do not belong to a valid group. |

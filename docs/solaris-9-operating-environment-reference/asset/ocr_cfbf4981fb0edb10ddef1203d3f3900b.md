# 744

# ls

+   -r Reverse the order of sort to get reverse alphabetic or oldest first as appropriate.

+   -R Recursively list subdirectories.

+   -s Give size in blocks, including indirect blocks, for each entry.

+   -t Sort by timestamp (latest first) instead of name. The default is the last modification time. (See -u and -c.)

+   -u Use time of last access instead of modification for sorting (with the -t option) or printing (with the -1 option).

+   -x Display multicolumn output, and sort entries across instead of down page.

+   -1 Print one entry per line of output.

Specifying more than one of the options in the following mutually exclusive pairs is not considered an error: -c and -1 (one), -c and -u. The last option specified in each pair determines the output format.

```
/usr/bin/ls
```

Specifying more than one of the options in the following mutually exclusive pairs is not considered an error: -c and -1 (ell), -m and -1 (ell), -x and -1 (ell), -@ and -1 (ell). The -1 option overrides the other option specified in each pair.

```
/usr/xpg4/bin/ls
```

Specifying more than one of the options in the following mutually exclusive pairs is not considered an error: -C and -1 (ell), -m and -1 (ell), -x and -1 (ell), -@ and -1 (ell). The last option specified in each pair determines the output format.

# Operands

+   file A path name of a file to be listed. If the specified file is not found, display a diagnostic message on standard error.

# Usage

ls(5) for the description of the behavior of ls when encountering files greater than or equal to 2 Gbytes (**31).

# Examples

The following example of file permissions describes a file that is readable, writable, executable by the user and readable by the group and others.

```
-rwsr-xr--
```

The following example describes a file that is readable, writable, executable by the user, readable and executable by the group, and enables its user ID to be assumed, during execution, by the user presently executing.

```
-rwsr-xr--
```

The following example describes a file that is readable only by the user and the group that can be locked during access.

```
-rw-r--r--
```
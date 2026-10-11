The user and group identifiers must be non-numeric. Attributes that do not need to be set by `%attr` may be replaced with a dash:

```
%attr(755, root, -) foo.bar
```

# E.6.1.4. The %verify Directive

The `%verify` directive is used to control which of nine different file attributes are to be verified by RPM. The attributes are

+   - `owner`—The file's owner.
+   - `group`—The file's group.
+   - `mode`—The file's mode.
+   - `md5`—The file's MD5 checksum.
+   - `size`—The file's size.
+   - `maj`—The file's major number.
+   - `min`—The file's minor number.
+   - `symlink`—The file's symbolic link string.
+   - `mtime`—The file's modification time.

One or more of these attributes may be listed in each `%verify` directive:

```
%verify(node md5 size maj min symlink mtime) /dev/ttyS0
```

If the keyword not precedes the list of attributes, every attribute except those listed will be verified.

# E.6.2. Directory-Related Directives

The directives outlined in the following sections modify `%files` list entries that are directories. For more information about these directives, see section 13.6.2 in Chapter 13.

# E.6.2.1. The %docdir Directive

The `%docdir` directive is used to add the specified directory to RPM's internal list of directories containing documentation. When a directory is added to this list, every file packaged in this directory (and any subdirectories) will automatically be marked as documentation.

# E.6.2.2. The %dir Directive

The `%dir` directive is used to direct RPM to package only the directory itself, regardless of what files may reside in the directory at the time the package is created:

```
%dir /usr/blahber
```
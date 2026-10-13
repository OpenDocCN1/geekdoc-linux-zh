+   - `.empty` — File is empty and is either a regular file or a directory.
+   - `.false` — Always false.
+   - `.fstype type` — File is on a file system of type *type*. The valid file system types vary among different versions of UNIX; an incomplete list of file system types that are accepted on one version of UNIX or another is: `ufs`, `4.2`, `4.3`, `nfs`, `tmp`, `mfs`, `S51K`, `S52K`. You can use `-printf` with the `%F` directive to see the types of your file systems.
+   - `.gid n` — Numeric group ID is *n*.
+   - `.group gname` — File belongs to group *gname* (numeric group ID allowed).
+   - `.iname pattern` — Like `-name`, but the match is not case sensitive.
+   - `.iname pattern` — Like `-name`, but the match is not case sensitive. For example, the patterns “foo” and “F??” match the filenames ‘Foo’, ‘FOO’, ‘foo’, ‘fOo’, and so forth.
+   - `.inum n` — File has inode number *n*.
+   - `.ipath pattern` — Like `-path`, but the match is not case sensitive.
+   - `.iregex pattern` — Like `-regex`, but the match is not case sensitive.
+   - `.links n` — File has *n* links.
+   - `.lname pattern` — File is a symbolic link whose contents match shell pattern *pattern*. The metacharacters do not treat `/` or `.` in a special way.
+   - `.mmin n` — File’s data was last modified *n* minutes ago.
+   - `.mtime n` — File’s data was last modified *n*24 hours ago.
+   - `.name pattern` — Base of filename (the path with the leading directories removed) matches shell pattern *pattern*. The metacharacters (`*`, `?`, and `[]`) do not match a `.` at the start of the base name. To ignore a directory and the files under it, use `-prune`; see an example in the description of `-path`.
+   - `.newer file` — File was modified more recently than *file*. `-newer` is affected by `-follow` only if `-follow` comes before `-newer` on the command line.
+   - `.nouser` — No user corresponds to file’s numeric user ID.
+   - `.nogroup` — No group corresponds to file’s numeric group ID.
+   - `.path pattern` — Filename matches shell pattern *pattern*. The metacharacters do not treat `/` or `.` in a special way; so, for example,
+     ```
+     find . -path './src*'
+     ```
+     will print an entry for a directory called `./src/misc` (if one exists). To ignore a whole directory tree, use `-prune` rather than checking every file in the tree. For example, to skip the directory `src/emacs` and all files and directories under it, and print the names of the other files found, do something like this:
+     ```
+     find . -path './src/emacs' -prune -o -print
+     ```
+   - `.perm mode` — File’s permission bits are exactly *mode* (octal or symbolic). Symbolic modes use mode `0` as a pointer of departure.
+   - `.perm -mode` — All the permission bits *mode* are set for the file.
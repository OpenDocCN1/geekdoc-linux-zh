+   - `-links num` This option searches for files that have *num* hard links.

+   - `-maxdepth depth` This option causes `find` to terminate its search after reaching *depth* directory levels, which can be useful to limit the search if you know the *file* wasn't buried too deeply in the directory tree.

+   - `-mtime time` This option works like `-atime`, but it uses the files' modification times.

+   - `-name pattern` This option searches for files based on the filename. The specified *pattern* may be a simple filename or it may contain various wildcards, such as asterisks (*) and question marks (?). You may need to enclose the *pattern* in quotation marks to keep the shell from expanding it, if you use wildcards.

+   - `-newer filename` You can find files that are newer than a specified other file with this option.

+   - `-perm [+|-]mode` Use this option if you want to find files that have a particular set of permissions. You can specify the *mode* as you would with *chmod*. If used without a plus or minus sign, this mode must be matched exactly. If you precede it with a plus sign, then *find* matches any file that includes *any* of the permission bits specified, even if others are also present. If you precede the *mode* with a minus sign, then *all* of the specified bits must be present, and others may be as well.

+   - `-size n[c]` You can find files based on their sizes with this option. Follow the size by a *c* character to find a file of a specific size in bytes, otherwise `find` locates files whose sizes match a number of 512-byte blocks.

+   - `-type file-type` This option locates files of a specified type. The *type-code* is the code listed in Table 8-1, with the addition of *f* for a regular file.

+   - `-user username` You can find files owned by a particular user with this option. The *username* can be specified as either a username or a UID.

These expressions are only some of the most useful for `find`. Consult the program's man page for more exotic options. Some examples of `find` in action include

```
```
$ find ./ -name "*.txt"
$ find /usr/local -perm +u+s
# find /etc -mtime -24h -name "*rc"
```
```

The first example finds all files in the current directory whose names end in *txt*. This is the sort of action that an ordinary user is likely to perform. The second example finds all the files in `/usr/local` that have their SUID bits set. Although an ordinary user can perform such a search, a system administrator is more likely to find this type of search useful, to help locate files that are set *SUID root*. The final example locates all files in the `/etc` directory tree whose names end in *rc* and that have been modified in the past 24 hours. An ordinary user can run such a command, but this example shows it as requiring *root* privileges because some directories in `/etc` aren't readable to
# chgrp

See Also

+   - eqn(1), nroff(1), troff(1), attributes(5), me(5), ms(5)

# chgrp — Change File Group Ownership

# Synopsis

```
/usr/bin/chgrp [-f -R] group file
```

# Description

You can use the chgrp command to change the group that owns a file, provided that you own the file and you are a member of the group that owns it. The chgrp command sets the group ID of the file named by each file operand to the group ID specified by the chgrp operand.

For each operand, chgrp performs actions equivalent to the chown(2) function, called with the following arguments:

+   - The file operand is used as the path argument.
- The user ID of the file is used as the owner argument.
- The specified group ID is used as the group argument.

Unless chgrp is invoked by a process with appropriate privileges, the set-user-ID and set-group-ID bits of all file groups are cleared upon successful completion; the set-user-ID and set-group-ID bits of other file types may be cleared.

The operating system has a {_POSIX_CHOWN_RESTRICTED} configuration option to restrict ownership changes. When this option is in effect, the owner of the file can change the group of the file only to a group to which the owner belongs. Only the superuser can arbitrarily change owner IDs, regardless of whether this option is in effect. To set this option, include the following line in /etc/system:

```
rstchown = 1
```

To disable this option, include the following line in /etc/system:

```
rstchown = 0
```

{_POSIX_CHOWN_RESTRICTED} is enabled by default. See system(2) and fpathconf(2).

# Options

+   -f Do not report errors.
-h If the file is a symbolic link, change the group of the symbolic link. Without this option, change the group of the file referenced by the symbolic link.
-R Recursively descend through the directory and any subdirectories, setting the specified group ID as chgrp proceeds. When chgrp encounters a symbolic link, change the group of the target file (unless you specify the -h option), but no recursion.
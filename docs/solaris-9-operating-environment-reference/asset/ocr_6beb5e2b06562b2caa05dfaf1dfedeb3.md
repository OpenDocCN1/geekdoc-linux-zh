pwait 1145

# pwait — Proc Tools

# Synopsis

```
/usr/proc/bin/pwait [-v] pid...
```

# Description

See proc(1).

# pwck, grpck — Password/Group File Checkers

# Synopsis

```
/usr/sbin/pwck [filename]
/usr/sbin/grpck [filename]
```

# Description

The pwck command scans the password file and notes any inconsistencies. The checks include validation of the number of fields, login name, user-to-use user ID, group ID, and whether the login directory and the program-to-use-as-shell exist. The default password grpck verifies all entries in the group file. This verification includes a check of the number of fields, group name, group ID, whether any login names belong to more than NGROUPS_MAX groups, and that all login names appear in the password file. The default group file is /etc/group.

> Note — If you specify no filename argument, grpck checks the local group file, /etc/group, and also makes sure that all login names encountered in the checked group file are known to the system getpwent(3C) routine. The login names may be supplied by a network nameservice.

# Files

```
/etc/group
/etc/passwd
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwcu |

# See Also

```
getpwent(3C), group(4), passwd(4), attributes(5)
```
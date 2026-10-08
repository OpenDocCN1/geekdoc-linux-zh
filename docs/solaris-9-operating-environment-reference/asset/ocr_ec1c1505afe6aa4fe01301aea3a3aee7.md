# 1172

/usr/xpg4/bin/rm

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcu4 |
| CSI | Enabled |

# See Also

rmdir(2), unlink(2), attributes(5), environ(5), largefile(5), XPG4(5)

# Diagnostics

All messages are generally self-explanatory.
You cannot remove the files . and . to avoid the consequences of inadvertently doing
sothing like the following.

```
castle@ -rm .*
```

# rmail — Read Mail or Send Mail to Users

# Synopsis

```
/usr/bin/rmail [-tw] [-m message-type] recipient...
```

# Description

See mail(1).

# rmdel — Remove a Delta from a SCCS

# Synopsis

```
/usr/ccs/bin/rmdel -rsid s.filename...
```

# Description

See sccs-rmdel(1).

# rmdir — Remove Directory Entries

# Synopsis

```
/usr/bin/rmdir [-ps] dirname...
```

# Description

See rm(1).
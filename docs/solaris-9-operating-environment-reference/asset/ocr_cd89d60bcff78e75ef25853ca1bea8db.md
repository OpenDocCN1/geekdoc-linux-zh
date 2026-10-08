# 246

# delta, sccs-delta

# Files

```
/etc/security/device_allocate
Mandatory access control information about each device.
/etc/security/device_maps
Access control information about each physical device.
/etc/security/dev/*
Lock files must exist for each allocatable device.
/etc/security/lib/*
Device allocate files.
```

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu |

# See Also

+   allocate(1), list_devices(1), bsmconv(1M), dminfo(1M), device_allocate(4), device_maps(4), attributes(5)

# delta, sccs-delta — Make a Delta to a SCCS File

# Synopsis

```
/usr/ccs/bin/delta [-g sid-list] [-gsid-list] [-m mr-list] [-mmr-list] [-r sid [-rsid] [-y[comment]] s.filename...
/usr/xpg4/bin/delta [-dnps] [-g sid-list] [-gsid-list] [-m mr-list | -mmr-list] [-r sid [-rsid] [-y[comment]] s.filename...
```

# Description

See sees-delta(1).

# deroff — Remove nroff/troff, tbl, and eqn Constructs

# Synopsis

```
/usr/bin/deroff [-m [m | s | 1]] [-w] [-i] [filename...]
```
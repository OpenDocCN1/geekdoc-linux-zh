# 418

# gencat

```
core.450: ELF 32-bit MSB core file SPARC Version 1, from 'cat'
castle%%
```

The following example tries to create a core image for process ID 461, which doesn't exist. Notice that gcore creates an output file named core.o, but it is an empty file.

```
castle%% gcore 461
castle%% ls -l *
-rw-rw-rw- 1 winsor 0 Jan 14 15:50 core.o
castle%%
```

# Exit Status

0 On success.
non-zero On failure, such as nonexistent process ID.

# Files

```
core.process-id
```

Core images.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNwtoo (32-bit)
SUNwtoox (64-bit) |

# See Also

```
kill(1), core(4), proc(4), attributes(5)
```

# gencat — Generate a Formatted Message Catalog

# Synopsis

```
/usr/bin/gencat catfile msgfile...
```

# Description

Use the gencat command to merge the message text source file(s) msgfileinto a formatted message database catfile does not already exist, it is created. If catfile exists, its messages are included in the new catfile. If set and message numbers collide, the new message text defined in msgfile replaces the old message text currently contained in catfile. The message text source file (or set of files) you input to gencat can contain either set and message numbers or simply message numbers, in which case the set NL_SETD (see nl_types(5)) is assumed.
# disable 265

# Operands

file A path name of an object file or an archive (see ar(1)) of objects.

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of dis: LC_CTYPE, LC_MESSAGES, and NLSPATH.

LIBDIR Use this as the path to search for the library. If the variable contains a null value or is not set, search for the library under /usr/lib.

# Exit Status

+   - 0 Successful completion.
- >0 An error occurred.

# Files

/usr/lib Default LIBDIR.

# Attributes

attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwtool |

# See Also

ar(1), as(1), ld(1), cc(1B), a.out(4), attributes(5), environ(5)

# Diagnostics

The self-explanatory diagnostics indicate errors in the command line or problems encountered with the specified files.

# disable — Disable LP Printers

# Synopsis

```
/usr/bin/disable [-c | -W] [-r [reason]] printer...
```

# Description

See enable(1).
# tcopy

# 1385

yields

| Town | Households Number | Size |
|---|---|--|
| Bedminster | 789 | 3.26 |
| Bernards Twp. | 3087 | 3.74 |
| Bernardsville | 2018 | 3.30 |
| Bound Brook | 3425 | 3.04 |
| Branchburg | 1644 | 3.49 |

# Files

```
/usr/share/lib/tmac/e
-me macros.
/usr/share/lib/tmac/m
-mm macros.
/usr/share/lib/tmac/s
-ms macros.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|--|
| Availability | SUNdoc |

# See Also

eqm(1), nroff(1), troff(1), attributes(5)

# tcopy - Copy a Magnetic Tape

# Synopsis

```
/usr/bin/tcopy source [destination]
```

# Description

Use the tcopy argument to copy the magnetic tape mounted on the tape drive specified by the source argument. The only assumption made about the contents of a tape is that there are two tape marks at the end.

When you specify only a source drive, tcopy scans the tape and displays information about the sizes of records and tape files. If you specify a destination, tcopy copies the source tape onto the destination, blocking preserved. As it copies, tcopy produces the same output as it does when scanning a tape.

Note - tcopy runs only on systems supporting an associated set of ioctl(2) requests.
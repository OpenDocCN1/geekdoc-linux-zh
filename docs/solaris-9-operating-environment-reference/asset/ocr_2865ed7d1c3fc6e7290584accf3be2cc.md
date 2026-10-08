# cksum

# Exit Status

0

The command executed successfully and all requested changes were made.

>0

An error occurred.

# Files

/etc/passwd

System password file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcs |
| CSI | Enabled |

> — chown is CSI-enabled except for the owner and group names.

# See Also

chgrp(1), chmod(1), chown(2), fpathconf(2), passwd(4), system(4), attributes(5), environ(5), largefile(5)

# cksum — Write File Checksums and Sizes

# Synopsis

```
/usr/bin/cksum [file...]
```

# Description

The cksum command calculates and writes to standard output a cyclic redundancy check (CRC) for each input file and also writes to standard output the redundancy of octets in each file.

For each file processed successfully, cksum writes in the following format:
"%u %d %s\n" checksum, # of octets, pathname

> If you do not specify a file operand, the path and leading space are omitted. The CRC is based on the polynomial used for CRC error checking in the referenced Ethernet standard.

The encoding for the CRC checksum is defined by the generating polynomial

```
G(x) = x32 + x26 + x23 + x22 + x16 + x12 + x11 + x10 + x8 + x7 + x4
+ x2 + x + 1
```
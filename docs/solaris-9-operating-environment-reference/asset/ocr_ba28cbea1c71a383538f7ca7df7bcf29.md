# sortbib

# 1303

# Exit Status

All input files were output successfully, or you specified -c and the input file was correctly sorted.

With the -c option, the file was not ordered as specified or, if you specified both the -c and -u options, two input lines were found with equal keys.

An error occurred.

+   0

+   1

+   >1

# Files

```
/var/tmp/stm???
```

Temporary files.

# Attributes

See attributes(5) for descriptions of the following attributes:

# /usr/bin/sort

| Attribute Type | Attribute Value |
| --- | --- |
| Availability CSI | SUMMesu Enabled |

# /usr/xpg4/bin/sort

| Attribute Type | Attribute Value |
| --- | --- |
| Availability CSI | SUMmxcu4 Enabled |

# See Also

comm(1), join(1), uniq(1), passwd(4), attributes(5), environ(5),
largefile(5), XPG4(5)

# Diagnostics

The sort command commands and exits with non-zero status for various trouble
conditions (for example, when input lines are too long) and for disorders discovered
under the -c option.

# sortbib — Sort a Bibliographic Database

# Synopsis

```
/usr/bin/sortbib [-s KEYS] database...
```

# Description

Use the sort command to sort files of records containing refer(1) keys by keys
y specify. Records can be separated by blank lines, or by . ( and .) delimiters, but the
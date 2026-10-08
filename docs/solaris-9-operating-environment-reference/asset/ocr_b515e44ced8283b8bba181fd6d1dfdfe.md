# 232

# Files

/etc/uucp/Devices
Device file.

/etc/uucp/Sysfiles
System file.

/etc/uucp/Systems
System file.

/var/spool/locks/*
Lock file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwnuu |

# See Also

cat(1), echo(1), stty(1), tip(1), uname(1), ct(1C), uuname(1C), uucp(1C), remote(4), attributes(5), environ(5)

System Administration Guide: IP Services

# cut — Cut Out Fields of Each Line of a File

# Synopsis

```
/usr/bin/cut -b list [-n] [file...]
/usr/bin/cut -c list [file...]
/usr/bin/cut -f list [-d delim] [-s] [file]
```

# Description

Use cut to cut out columns from a table or fields from each line of a file; parlance, cut implements the projection of a relation. The fields as specified by list can be fixed length, is character positions on a punched card (-c option), or the length vary from line to line and be marked with a field delimiter character like Tab (-f option). You can use cut as a filter.

> Note — You must specify the -b, -c, or -f option.

Use grep(1) to make horizontal cuts (by context) through a file, or paste(1) to put files together column-wise (that is, horizontally). To reorder columns in a table, use cut and paste. *
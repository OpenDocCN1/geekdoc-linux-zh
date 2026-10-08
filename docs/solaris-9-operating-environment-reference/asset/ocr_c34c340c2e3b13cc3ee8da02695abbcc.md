736

ipstat

# Examples

The following example removes request-ID385 from destination killtree.

```
castle% lprm -P killtree 385
```

# Exit Status

+   - 0 Successful completion.

+   - non-zero An error occurred.

# Files

```
/var/spool/print/[cd]*
```

Spooling directories and files.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNscplp |

# See Also

lp(1), lpstat(1), lpc(1B), l1q(1B), lpr(1B), lpadmin(1M),
sswitch.conf(4), printers(4), printers.conf(4), attributes(5),
standards(5)

# Ipstat — Display Information About the Status of the Print

Service

# Synopsis

```
/usr/bin/lpstat [-d] [-r] [-s] [-t] [-a [list] [-c [list]
-f [list] [-l] [-o [list] [-p [list] [-D] [-S [list] [-1]
-u [login-ID-list] [-v [list]]
```

# Description

lpstat displays information about the current status of the LP print service to standard
output.

If you specify no options, lpstat prints the status of all your print requests made by\lp(lp(1)). Any arguments that are not options are assumed to be request-ID as
returned by lpstat. The lpstat command prints the status of such requests. You can specify
options in any order and can interplex them with other arguments. You can
follow some key letters with an optional list that can be in of two forms: a list of
items separated from one another by a comma, or a list of items separated from one
an spaces enclosed in quotes. For example:

```
castle% lpstat - *user user2 user3
```
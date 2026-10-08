# awk

# 87

# Files

/etc/user_attr

RBAC extended user attributes database.

/etc/security/auth_attr

RBAC authorization descriptions database.

/etc/security/policy.conf

Configuration file for security policy.

/etc/security/prof_attr

RBAC profile description database

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNMcsu |

# See Also

profiles(1), roles(1), getauthattr(3SEDB), auth_attr(4), policy.conf(4), prof_attr(4), user_attr(4), attributes(5)

# awk — Pattern Scanning and Processing Language

# Synopsis

```
/usr/bin/awk [-f profile] [-Fc] ['prog'] [parameters] [filename...]
/usr/xpq4/bin/awk [-F ERE] [-v assignment...] 'program' | -f profile...
[argument...]
```

# Description

The awk command is a programming language that is very useful for computation and pattern matching. The name awk is an acronym composed of the initials of its developers of the language: Aw, Weiner, and Kernighan. The /usr/xpq4/bin/awk command is described on the awk(1) manual page. The awk is a greatly enhanced and optimized version of awk.

The /usr/bin/awk command scans a list of input files for lines that match any set of patterns specified in prog. The programming must be enclosed in single quotes ('') to protect it from the shell. For each pattern in prog there may be an associated action performed when a line of file matches the pattern. The set of pattern-action statements may appear literally as prog in a file specified with the -f profile input. Input files are read in order; if there are no files, the standard input is read. The file-name dash (—) means the standard input.
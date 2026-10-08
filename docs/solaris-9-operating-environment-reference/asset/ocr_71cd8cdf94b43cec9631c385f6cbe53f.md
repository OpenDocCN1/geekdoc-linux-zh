# spline 1309

castle$

# Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of spell: LC_CTYPE, LC_MESSAGES, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Files

+   D_SPELL=/usr/lib/spell/hlist[ab]
Hashed spelling lists, American and British.
S_SPELL=/usr/lib/spell/hstop
Hashed stop list.
H_SPELL=/var/adm/spellhist
History file.
/usr/share/lib/dict/words
Master dictionary.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | Sunmesu |

# See Also

deroff(1), eqn(1), sort(1), tbl(1), stoff(1), attributes(5), environ(5)

# Bugs

The spelling list's coverage is uneven; new installations may want to monitor the output for several months to gather local additions.
British spelling was compiled by an American.

# spline — Interpolate Smooth Curve

# Synopsis

```
/usr/bin/spline [-akmnx]...
```

# Description

The spline command takes pairs of numbers from the standard input as abscissas and ordin of a function. It produces a similar set, which is approximately equally spaced
# xstr 1567

-v Display a progress report indicating where new or duplicate strings are found.

# Files

+   - Strings Database of strings.
- x.c Massaged C source.
- xs.c C source for definition of array "xstr" (rq).
- /tmp/xs* Temporary file when xstr file name doesn't touch strings.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNMcsu |

# See Also

make (1S), attributes (5)

# Bugs

If a string is a suffix of another string in the database and the shorter string is seen by xstr, both strings are placed in the database when just placing the longer one there would suffice.
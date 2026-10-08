# and look for more empty lines.
:Empty

```
/^S/    (
    N
ns//
b Empty
)
# Write the nonempty line before going back to search
# for the first in a set of empty lines.
p    
```

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of sed: LC_COLLATE, LC_CTYPE, LC_MESSAGES, and NLSPATH.

# Exit Status

+   - 0 Successful completion.
- >0 An error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes:

# /usr/bin/sed

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwcsu |
| CSI | Not enabled |

# /usr/xpg4/bin/sed

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNwccu4 |
| CSI | Enabled |

# See Also

awk(1), ed(1), grep(1), attributes(5), environ(5), largefile(5), regexp(5), XPG4(5)
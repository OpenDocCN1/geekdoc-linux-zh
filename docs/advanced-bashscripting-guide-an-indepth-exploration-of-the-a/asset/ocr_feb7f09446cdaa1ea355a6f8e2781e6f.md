# Advanced Bash–Scripting Guide

Clever combinations of "and" and "or" lists are possible, but the logic may easily become convoluted and require extensive debugging.

```
false && true || echo false    # false

# Same result as
( false && true ) || echo false    # false
# But not*
false && ( true || echo false )      # (nothing echoed)

# Note left-to-right grouping and evaluation of statements,
since the logic operators "&&" and "||" have equal precedence.

# It's best to avoid such complexities, unless you know what you're doing.

# Thanks, S.C.
```

See Example A–7 for an illustration of using an and / or list to test variables.
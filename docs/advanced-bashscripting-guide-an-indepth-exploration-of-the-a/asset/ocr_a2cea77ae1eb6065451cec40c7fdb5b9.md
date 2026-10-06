# Advanced Bash–Scripting Guide

```
# grep PATTERN /etc/passwd | awk -F:"' '{ print $5 )'
# or awk -F:/PATTERN/ (print $5 )
# or or awk -F: '{$1 == "username" { print $5 }' # real name from username
# However, it might not be as instructive.

exit 0
```

There is an alternative, and perhaps less confusing method of redirecting a function's stdin that involves redirecting the stdin to an embedded bracketed code block within the function.

```
# Instead of:
Function ()
{
  ...
} < file

# Try this:
Function ()
{
  ...
  } < file

# Similarly,
Function () # This works.
{
  echo $* 
} | tr a b


Function () # This doesn't work.
{
  echo $* 
} | tr a b # A nested code block is mandatory here.
```

```
# Thanks, S.C.
```

# 23.2. Local Variables

What makes a variable "local"?

local variables

A variable declared as local is one that is visible only within the block of code in which it appears. It has local "scope". In a function, a local variable has meaning only within that function block.

Example 23–8. Local variable visibility

```
#!/bin/bash
```

23.2. Local Variables
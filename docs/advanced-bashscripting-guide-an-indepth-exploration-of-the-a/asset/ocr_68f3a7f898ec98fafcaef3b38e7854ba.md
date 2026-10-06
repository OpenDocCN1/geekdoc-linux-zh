# Advanced Bash–Scripting Guide

```
echo "${0##*/}"      # Name of script.
echo
filename=test.data          # data
echo "${filename##*.}"    # Extension of filename.
```

$($varpattern), ${(varpattern)

Remove from var the shortest/longest part of $pattern that matches the back end of $var.

Version 2 of Bash adds additional options.

# Example 9–14. Pattern matching in parameter substitution

```
#!/bin/bash
# Pattern matching using the # and % parameter substitution operators.
var1=abcd12345abc6789
pattern1=*c # (wild) matches everything between a - c.

echo var="$var1" # abcd12345abc6789
echo "$var1" (alternate form) abcd12345abc6789
echo "Number of characters in ${var1}" = ${#var1}
echo pattern1=$*c (everything between 'a' and 'c')
echo
```

```
echo "${var1$pattern1}" = '${var1$pattern1}\' # dcd12345abc6789
# Shortest possible match, strips out first 3 characters abcd12345abc6789
^^^^
echo '${var1#$pattern1}' = '${var1#$pattern1}\' # 6789
# Longest possible match, strips out first 12 characters abcd12345abc6789
^^^^^^^^^^^^^^^^
```

```
echo;
pattern2=b*9 # everything between 'b' and '9'
echo var="$var1" # Still abcd12345abc6789
echo pattern2=$pattern2
echo
```

```
echo "${var1%pattern2}" = '${var1%pattern2}\' # abcd12345a
# Shortest possible match, strips out 6 characters abcd12345abc6789
^^^^^^
echo '${var1%%pattern2}' = '${var1%%pattern2}\' #
# Longest possible match, strips out last 12 characters abcd12345abc6789
^^^^^^^^^^^^^^^^
```

# Remember, and # ## work from the left end of string,
# % and %% work from the right end.

```
echo
exit 0
```

# Example 9–15. Renaming file extensions:

```
#!/bin/bash
```

# 9.3. Parameter Substitution
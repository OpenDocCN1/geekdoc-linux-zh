# Advanced Bash–Scripting Guide

```
echo "Substring of \$a\", starting at position 2, and 6 chars long is \"$b\"

# 'match' operations similarly to 'grep'
# uses Regular Expressions
b=expr match "\$a" '[0-9]*'
echo Number of digits at the beginning of \"$a\" is $b
b=expr match "\$a" '\([0-9]*' # Note escaped parentheses.
echo "The digits at the beginning of \"$a\" are \"$b\"

echo

exit 0
```

The , operator can substitute for match. For example, b=expr $a : [0-9]* is
equivalent of b=expr match $a [0-9]* in the above listing.

```
#!/bin/bash
echo
echo "String operations using \$expr $string string:\" construct"
echo
-----------------
a1234zipper43231
echo "The string being operated upon is \"expr \$a\" : '\(.*\)\'\""
# Escaped parentheses.
Regular expression parsing.
echo "Length of \"$a\" is \"expr \$a\" : '.*' # Length of string
echo "Number of digits at the beginning of \"$a\" is \"expr \$a\" : '[0-9]*'"
echo "The digits at the beginning of \"$a\" are \"expr \$a\" : '\([0-9]*\)\'"

echo

exit 0
```

Perl and sed have superior string parsing facilities. A short Perl or sed "subroutine" within a script (see Section 34.2) is an attractive alternative to using expr.

See Section 9.2 for more string operations.

# 12.3. Time / Date Commands

Command Listing

```
date
```

Simply invoked, date prints the date and time to stdout. Where this command gets interesting is in its formatting and parsing options.

12.3. Time / Date Commands

150
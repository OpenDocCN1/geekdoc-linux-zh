# Advanced Bash-Scripting Guide

```
echo "Positional parameters before set \`uname -a\` : $"
echo "Command-line argument #1 = $1"
echo "Command-line argument #2 = $2"
echo "Command-line argument #3 = $3"
```

```
set `uname -a` # Sets the positional parameters to the output
echo # of the command uname -a
```

```
echo
echo +++++
echo $-
# +++++
# Flags set in script.
echo $-
# hB
anomalous behavior?
echo
```

```
echo "Positional parameters after set \`uname -a\` : $"
# $1, $2, $3, reinitialized to result of \`uname -a\"
echo "Field #1 of \`uname -a\` = $1"
echo "Field #2 of \`uname -a\` = $2"
echo "Field #3 of \`uname -a\` = $3"
echo \##\$
# ###
```

```
exit 0
```

More fun with positional parameters.

# Example 15-17. Reversing the positional parameters

```
#!/bin/bash
# reverseposparams.sh: Reverse positional parameters.
# Script by Dan Jacobson, with stylistic revisions by document author.
```

```
set a\b c d e;
^ Spaces escaped
^ Spaces not escaped
OIFS=$IFS; IFS=$-;
^ Saving old IFS and setting new one.
```

```
echo
until [ $# -eq 0 ];
do # Step through positional parameters.
echo "$### k0 = \$k\" # Before
k=$1;$k
 # Append each param to loop variable.
echo "$### k = \$k\" # After
echo
shift
done
```

```
set $k # Set new positional parameters.
echo
echo $* # Count of positional parameters.
echo -
```

15. Internal Commands and Builtins
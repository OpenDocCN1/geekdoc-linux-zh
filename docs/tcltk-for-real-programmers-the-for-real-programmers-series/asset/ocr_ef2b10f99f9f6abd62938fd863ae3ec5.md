# Example 4.2.2-2

```
set x 2
set y 3
puts "The sum of $x and $y is returned by [expr $x+$y]"
```

# Script Output

The sum of 2 and 3 is returned by 5

In Example 4.2.2-3, the argument is enclosed in quotes, so substitution occurs, but the square brackets are escaped with backslashes to prevent Tcl from performing a command substitution.

# Example 4.2.2-3

```
set x 2
set y 3
puts "The sum of $x and $y is returned by \[expr $x+$y\]"
```

# Script Output

The sum of 2 and 3 is returned by [expr 2+3]

Example 4.2.2-4 escapes the dollar sign on the variables to prevent them from being substituted and also escapes a set of quotes around the expr string. If not for the backslashes before the quotes, the quoted string would end with the second quote. Sets of brackets nest, whereas quotes do not.

# Example 4.2.2-4

```
set x 2
set y 3
puts "The sum of \$x \$y is returned by \"[expr \$x+\$y]\""
```

# Script Output

The sum of $x + $y is returned by "[expr $x+$y]"

# 4.2.3 Steps in Command Evaluation

When a Tcl interpreter evaluates a command, it makes only one pass over that command to do substitutions. It does not loop until a variable is fully resolved. However, if a command includes another Tcl command within
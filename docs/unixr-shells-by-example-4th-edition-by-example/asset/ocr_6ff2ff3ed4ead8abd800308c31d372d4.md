# EXAMPLE 11.32 (CONTINUED)

```
2  $ print $1        # Prints the first position.
    tim

3  $ print $2 $3     # Prints the second and third position.
    bill ann

4  $ print $#        # Prints the total number of positional parameters.
    4

5  $ set a b c d e f g h i j k l m
    $ print $10      # Prints the first positional parameter followed by a 0.
    a0
    $ print ${10} ${11} # Prints the 10th and 11th positions.
    j k

6  $ print $#
    13

7  $ print $*
    a b c d e f g h i j k l m

8  $ set file1 file2 file3
    $ print \$$#
    $3

9  $ eval print \$$#
    file3
```

# EXPLANATION

+   1 The set command assigns values to positional parameters. The $* special variable contains all of the parameters set.
+   2 The value of the first positional parameter, tim, is displayed.
+   3 The value of the second and third parameters, bill and ann, are displayed.
+   4 The $# special variable contains the number of positional parameters currently set.
+   5 The set command resets all of the positional parameters. The original parameter list is cleared. To print any positional parameters beyond 9, the curly braces are used to keep the two digits together. Otherwise, the value of the first positional parameter is printed, followed by the number appended to it.
+   6 The number of positional parameters is now 13.
+   7 The values of all of the positional parameters are printed.
+   8 The dollar sign is escaped; $# is the number of arguments. The print command displays $3, a literal dollar sign followed by the number of positional parameters.
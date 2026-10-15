# EXPLANATION

With the -b option, grep prints the byte offset from the input file before each line of output.

Instead of using the datafile for these next two examples, we'll use a file called negative to demonstrate the -e and -x options.

```
% cat negative
-40 is cold.
This is line 1.
This is line 2.5
-alF are options to the ls command
```

# EXAMPLE 4.65

```
1 % grep -e "-aIF" negative
-aIF are options to the ls command
```

```
2 % grep --regexp=-40 negative
-40 is cold.
```

# EXPLANATION

+   1. With the -e option, grep treats all characters in the pattern equally, so that leading dashes are not mistaken for options.
+   2. The alternate way to represent -e is --regexp=pattern, where pattern is the regular expression; in this example the regular expression is -40.

# EXAMPLE 4.66

```
% grep -x -e "-40 is cold." negative
-40 is cold.
```

# EXPLANATION

With the -x option, grep will not match a line unless the search pattern is identical to the entire line. The -e is used to allow a dash as the first character in the search string.
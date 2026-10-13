An example of the latter is the following:

```
$ cat countfiles
#!/bin/sh

# countfiles - return a count of the files matching the specified pattern

pattern="${1:-dave}"
locate=/usr/bin/locate

for name in `locate $pattern`
do
  count=`expr ${count:-0} + 1`
done

echo "I counted $count files that matched pattern $pattern"

exit 0
```

This is an interesting script, because it has variables performing three different functions: locate is a constant that makes it easy to reconfigure the script for different Unixes that have the locate command in odd places (or not at all, perhaps replacing it with a find). The count variable is a numeric counter that increments by one each time it's referenced in the line:

`count=`expr ${count:-0} + 1` `

The pattern variable holds the filename pattern that's being counted, or, if no value is initially specified on the command line, dave as the default pattern.

The unusual notation of ${variable:-default} should be read as a very convenient shorthand for the following logic: if $variable is defined, then $variable; otherwise the default value $default. In the initial assignment to pattern, you can now see that the line

`pattern="${1:-dave}"`

really means "let pattern equal $1 if the user specified a pattern on the command line, otherwise use the default pattern dave."

5. This shell script also demonstrates that you can use the helpful expr command for simple math functions, particularly within shell scripts.

For example, here's a variation on the preceding shell script that calculates the total number of lines, and the average number of lines per file as well:

```
$ cat countfiles
#!/bin/sh

# countfiles - return a count of the files matching the specified pattern,
# and average line counts too.
```
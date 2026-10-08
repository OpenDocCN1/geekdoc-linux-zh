# grep 473

Match, using fixed strings. Treat each pattern specified as a string instead of a regular expression. If an input line contains any of the patterns as a contiguous sequence of bytes, match the line. A null string matches every line. See grep(1) for more information.

-F

-q

Do not write anything to the standard output, regardless of matching lines. Exit with 0 status if an input line is selected.

-x

Consider only input lines that use all characters in the line to match an entire fixed string or regular expression to be matching lines.

# Operands

file

A name of a file to be searched for the patterns. If no file operands are specified, use the standard input.

```
/usr/bin/grep pattern
```

Specify a pattern to be used during the search for input.

```
/usr/xpg4/bin/grep pattern
```

Specify one or more patterns to be used during the search for input. This operand is treated as if were specified as -e pattern-list.

# Usage

The -e pattern-list option has the same effect as the pattern-list operand but is useful when pattern-list begins with the hyphen delimiter. It is also useful when it is more convenient to provide multiple patterns as separate arguments.

grep accepts multiple -e and -f options uses all of the patterns it is given to match input lines.

> Note The order of evaluation is not specified. If an implementation finds a null string as a pattern, it is allowed to use that pattern first, matching every line, and effectively ignore any other patterns.

> The -q option provides a means of determining whether or not a pattern (or string) exists in a group of files. When searching several files, it provides a performance improvement (because grep can quit as soon as it finds the first match) and requires less care by the user in choosing the set of files to supply as arguments (because grep exits if it finds a match even grep detected an access or read on earlier file operands).

# Large File Behavior

See grep(5) for the description of the behavior of grep when encountering files greater than or equal to 2 Gbytes (**31 bytes).

# Examples

The following example finds all of the word POSIX in the manual page and displays the line with a line number preceding it. To save space, not all of the lines are shown in this example.

```
castle@/usr/bin/grep -i n posix standards.5
```

```
7:standards, posix, POSIX, posix.1, POSIX.1, posix.2, POSIX.2, xnet, XNET, xnet4, XNET4, xpg, XPG, xpg3, XPG3, xpg4, XPG4, xpgv2, standards and the new *
```
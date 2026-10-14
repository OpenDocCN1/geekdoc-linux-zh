# B.6.2  Substituting on a Specific Line

To make a substitution on a specific line, use a subcommand of the following form:

```
`n s/ oldstring / newstring /`
```

Here n is the number of the line on which the substitution is to be made. In the following example, the s subcommand moves to line number 1 and replaces the string "stop" with the string "quit" and displays the new line:

```
1s/stop/quit/p
The only way to quit
_
```

The s subcommand changes only the first occurrence of the string on a given line. To learn how to change all occurrences of a string on the line, see Section B.6.4.

# B.6.3  Substituting on Multiple Lines

To make a substitution on multiple lines, use a subcommand of the following form:

```
`n,m s/ oldstring / newstring /`
```

Here n is the first line of the group and m is the last. In the following example, the s subcommand replaces the first occurrence of the string "to" with the string "TO" on every line in the buffer:

```
1,$s/to/TO/
^$p
The only way TO quit
adding text is TO enter a
line that contains only
a dot.
_
```

The 1,$p subcommand displays the contents of the buffer, which lets you verify that the substitutions were made.

# B.6.4  Changing Every Occurrence of a String

Ordinarily, the s (substitute) subcommand changes only the first occurrence of a string on a given line. However, the g (global) operator lets you change every occurrence of a string on a line or in a group of lines.

To make a global substitution on a single line, use a subcommand of the following form:

```
`n s/ oldstring / newstring /`
```
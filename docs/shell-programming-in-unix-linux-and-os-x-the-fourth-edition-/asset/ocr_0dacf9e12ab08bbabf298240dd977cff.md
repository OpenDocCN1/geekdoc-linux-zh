# The regular expression

`.x.`

matches an **x** that is surrounded by any two characters, not necessarily the same.

We can demonstrate a lot of regular expressions by using the simple ed editor, an old-school line-oriented editor that has been around as long as Linux have been around.

For example, the ed command

```
```text
/ ... /
```
```

searches forward in the file you are editing for the first line that contains any three characters surrounded by blanks. But before we demonstrate that, notice in the very beginning of this example that ed shows the number of characters in the file (248) and that commands like print (p) can be prefixed with a range specifier, with the most basic being `1,$`, which is the first through last line of the file:

```
```text
$ ed intro
248
1,$p
The Unix operating system was pioneered by Ken
Thompson and Dennis Ritchie at Bell Laboratories
in the late 1960s. One of the primary goals in
the design of the Unix system was to create an
environment that promoted efficient program
development.
```
```

*Print all the lines*

That’s our working file. Now let’s try some regular expressions:

```
```text
/ ... /
The Unix operating system was pioneered by Ken
/
Thompson and Dennis Ritchie at Bell Laboratories
1,$s/p.o/XXX/g
1,$p
The Unix operating system was XXXneered by Ken
ThomXXXn and Dennis Ritchie at Bell Laboratories
in the late 1960s. One of the primary goals in
the design of the Unix system was to create an
environment that XXXmoted efficient XXXgram
development.
```
```

*Look for three chars surrounded by blanks*

*Repeat last search*

*Change all p.os to XXX*

*Let’s see what happened*

In the first search, ed started searching from the beginning of the file and found that the sequence “was” in the first line matched the indicated pattern and printed it.

Repeating the search (the ed command `/`) resulted in the display of the second line of the file because “and” matched the pattern. The substitute command s that followed specified that all occurrences of the character p, followed by any single character, followed by the character o were to be replaced by the characters XXX. The prefix `1,$` indicates that it should be applied to all lines in the file, and the substitution is specified with the structure `s/old/new/g`, where a
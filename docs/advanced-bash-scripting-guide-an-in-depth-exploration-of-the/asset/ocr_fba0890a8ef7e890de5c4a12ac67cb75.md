# # Advanced Bash-Scripting Guide

| s/0*/0/g necho "Working on it." | sed -e 'li How far are you along?'
5i 'Linux is great.' file.txt
| Compress consecutive sequences of zeroes
into a single zero.
Prints "How far are you along?" as first line,
"Working on it" as second.
Inserts 'Linux is great.' at line 5 of the file
file.txt.
Delete all lines containing 'GUI'.
| /GUI/
s/GUI//
Delete all instances of "GUI", leaving the
remainder of each line |

Substituting a zero-length string for another is equivalent to deleting string until line of input. This leaves the remainder of the line intact. Applying s/GUI// to the line

| The most important parts of any application are its GUI and sound effects results in |
The most important parts of any application are its and sound effects |

A backslash forces the sed replacement to continue to the next line. This has the effect of using the newline at the end of the first line as the replacement string.

```
s/^\**/ /g
```

This substitution replaces line-beginning spaces with a newline. The net result is to replace paragraph indents with a blank line between paragraphs.

 address followed by one or more operations may open and closed curly brackets, with appropriate newlines.

```
/[0-9A-Za-z]/,/S{/
^d/
```

This deletes the first line of each blank line. That might be useful for single-spacing a text file, by retaining the blank line(s) between paragraphs.

> The delimiter that sed uses is /. However, sed allows other delimiters, such as :). This is useful when / is part of a replacement string, as in a filename. Example 11-10 and Example 16-32.

> A quick way to double-space a text file is sed G filename.
For illustrative of sed within shell scripts:

+   1. Example 36-1
2. Example 36-2
3. Example 16-3
4. Example A-2
5. Example 16-17
6. Example 16-27
7. Example A-12
8. Example A-16
9. Example A-17
10. Example 16-32
11. Example 11-10

Appendix C. A Sed and Awk Micro-Primer
# Appendix Summary

A regular expression defines a set of one or more strings of characters. A regular expression is said to match any string it defines.

# Special Characters

| | |
| * | Matches any single character |
| ^ | Matches zero or more occurrences of a match of the preceding character |
| | Forces a match to the beginning of a line |
| $ | A match to the end of a line |
| \| | Used to quote special characters |
| \< | Forces a match to the beginning of a word |
| \> | Forces a match to the end of a word |

# Character Classes and Bracketed Regular Expressions

| | |
| [xyz] | Defines a character class that matches x, y, or z |
| [^ xyz] | Defines a character class that matches any character except x, y, or z |
| [x-z] | Defines a character class that matches any character x through z inclusive |
| (xyz) | Matches what xyz matches (a bracketed regular expression) |

# Extended Regular Expression

In addition to the preceding special characters and strings (excluding quoted parentheses, except in vim), the following characters are special within full, or extended, regular expressions.
# APPENDIX SUMMARY

A regular expression defines a set of one or more strings of characters. A regular expression is said to match any string it defines.

In a regular expression, a special character is one that does not represent itself. Table A-9 lists special characters.

Table A-9 Special characters

| Character | Meaning |
| :--- | :--- |
| `.` | Matches any single character |
| `*` | Matches zero or more occurrences of a match of the preceding character |
| `^` | Forces a match to the beginning of a line |
| `$` | A match to the end of a line |
| `\` | Quotes special characters |
| `\<` | Forces a match to the beginning of a word |
| `\>` | Forces a match to the end of a word |

Table A-10 lists ways of representing character classes and bracketed regular expressions.

Table A-10 Character classes and bracketed regular expressions

| Class | Meaning |
| :--- | :--- |
| `[xyz]` | Defines a character class that matches `x`, `y`, or `z` |
| `[^xyz]` | Defines a character class that matches any character except `x`, `y`, or `z` |
| `[x-z]` | Defines a character class that matches any character `x` through `z` inclusive |
| `\(xyz\)` | Matches what `xyz` matches (a bracketed regular expression; not Perl) |
| `(xyz)` | Matches what `xyz` matches (a bracketed regular expression; Perl only) |

In addition to the preceding special characters and strings (excluding quoted parentheses, except in vim), the characters in Table A-11 are special within full, or extended, regular expressions.

Table A-11 Extended regular expressions

| Expression | Matches |
| :--- | :--- |
| `+` | One or more occurrences of the preceding character |
| `?` | Zero or one occurrence of the preceding character |
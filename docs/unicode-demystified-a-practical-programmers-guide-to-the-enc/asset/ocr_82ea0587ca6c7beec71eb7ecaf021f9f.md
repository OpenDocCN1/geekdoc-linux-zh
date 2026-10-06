# Caret and Dollar Sign

A regular expression that begins with a caret (^) can match a string only at the beginning of a line. In a similar manner a dollar sign at the end of a line of regular expression matches the end of a line. The caret and dollar sign are called anchors because they force (anchor) a match to the beginning or end of a line (Table A-5).

# Quoting Special Characters

You can quote any special character (but not a digit or parenthesis) by preceding it with a backslash (Table A-6). Quoting a special character makes it represent itself.

| Regular Expression | Matches | Table A-6 Examples |
| --- | --- | --- |
| /end\/ | All strings that contain end followed by a period | end., send., pretend,mail |
| \\ | A single backslash | \
| /\*/ | An asterisk | \*c, an asterisk (*) |
| \[5\]/ | [5] | it was five [5] |
| /and \or/ | and/or | and/or |

# Rules

The following rules govern the application of regular expressions.

# Longest Match Possible

As stated previously, a regular expression always matches the longest possible string, starting as far toward the beginning of the line as possible. For example, given the following string,

> This (rug) is not what it once was (a long time ago), is it?

the expression /Th.*is*/ matches

This (rug) is not what it once was (a long time ago), is
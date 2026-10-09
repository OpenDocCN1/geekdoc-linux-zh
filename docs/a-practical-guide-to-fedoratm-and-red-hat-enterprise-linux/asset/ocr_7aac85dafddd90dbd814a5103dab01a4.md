# QUOTING SPECIAL CHARACTERS

You can quote any special character (but not parentheses [except in Perl] or a digit) by preceding it with a backslash (Table A-6). Quoting a special character makes it represent itself.

Table A-6 Quoted special characters

| Regular expression | Matches | Examples |
| :--- | :--- | :--- |
| /end\./ | All strings that contain end followed by a period | The end., send., pretend,mail |
| /\\/ | A single backslash | \\ |
| /\*/ | An asterisk | *, an asterisk (*) |
| /\[5\]\./ | [5] | it was five [5] |
| /and\/or/ | and/or | and/or |

# RULES

The following rules govern the application of regular expressions.

# LONGEST MATCH POSSIBLE

A regular expression always matches the longest possible string, starting as far toward the beginning (left end) of the line as possible. Perl calls this type of match a *greedy match*. For example, given the string

```
This (rug) is not what it once was (a long time ago), is it?
```

the expression `/Th.*is/` matches

```
This (rug) is not what it once was (a long time ago), is
```

and `/(.*)/` matches

```
(rug) is not what it once was (a long time ago)
```

However, `/(.*)/` matches

```
(rug)
```

Given the string

```
singing songs, singing more and more
```

the expression `/.s.*ing/` matches

```
singing songs, singing
```

and `/.s.*ing song/` matches

```
singing song
```
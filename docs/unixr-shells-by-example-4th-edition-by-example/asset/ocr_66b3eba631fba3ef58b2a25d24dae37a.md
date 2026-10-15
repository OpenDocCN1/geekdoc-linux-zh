# SUPPORTED REGULAR EXPRESSIONS:

|  |  |
|---|---|
| . | Matches any character except newline. |
| \d | Matches any digit. |
| \e | Matches ESC char. |
| * | Matches zero or more occurrences of previous RE. |
| + | Matches one or more occurrences of previous RE. |
| ? | Matches zero or one occurrence of previous RE. |
| ^ | Matches beginning of line. |
| $ | Matches end of line. |
| [ ... ] | Matches any single character between brackets. For example, [-0-24&8] matches - or any even digit, and [-0-9a-z] matches - and any digit between 0 and 9 as well as letters a through z. |
| \{ ... \} | Used for repetition; e.g., x\{9\} matches nine x characters |
| \( ... \) | Used for backreferencing. Pattern in \( ... \) is tagged and saved. Starting at the left-hand side of the regular expression, allowed up to nine tags. To restore saved pattern, \1, \2 ... \9 are used. |
| \2 \1, ..., \9 | Matches match specified by nth \( ... \) expression. For example, \([\t][a-zA-Z]+\)/\1[\t] matches any word repeated consecutively. |

# EXAMPLE A.45

```
1  rgrep -n -R '*.c' 'A'int'
2  rgrep -n -xc 'A'int'
```

# EXPLANATION

+   1. Look in all files with a "c" extension in current directory and all its subdirectories looking for matches of "int" at the beginning of a line, printing the line containing the match with its line number.
+   2. Look in all files with a ".c" extension, printing the line beginning with "int" and preceded with its line number. (Same as above.)

# rlogin—remote login

```
rlogin [-l ] [-8 ] [-ec ] [-l username ] hostname
```

rlogin establishes a remote login session from your terminal to the remote machine named hostname. Hostnames are listed in the host's database, which may be contained in the /etc/hosts file, the Network Information Service (NIS) hosts map, the Internet
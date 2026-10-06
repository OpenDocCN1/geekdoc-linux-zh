# Exercises 833

| | |
|---|---|
| ESCAPE U | Changes next word to all uppercase |
| ESCAPE . | Inserts last word from previous command line before current character |

# History Editing Commands (emacs)

| | |
|---|---|
| CONTROL-P | Moves to previous line in history file |
| CONTROL-N | Moves to next line in history file |
| ESCAPE< | Moves to first line in history file |
| ESCAPE> | Moves to last line in history file |
| CONTROL-R string | Search backward for string |

# Miscellaneous Commands (emacs)

| | |
|---|---|
| ESCAPE = | Lists pathnames that match current word (pathname listing) |
| ESCAPE ESCAPE | Completes current word to a unique or partial pathname (pathname completion) |
| ESCAPE* | Expands current word to all matching pathnames (pathname expansion) |
| CONTROL-U | Repeats next command four times |
| CONTROL-V | Displays the current version of the Z Shell |
| CONTROL-L | Redisplays the current line |

# Exercises

1. The dirname utility treats its argument as a pathname and writes to standard output the path prefix, that is, everything up to but not including the last component. Thus
dirname a/b/c/d
writes a/b/c to standard output. If path is a simple filename (has no / characters), dirname writes a . to standard output.
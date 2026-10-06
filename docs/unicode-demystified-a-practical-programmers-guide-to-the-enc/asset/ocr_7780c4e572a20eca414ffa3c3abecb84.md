# Chapter Summary 831

| D | Deletes from current character to end of line |
| dd | Deletes entire command |
| C | Changes from current character to end of line |

# History Editing Commands (vi)

| j | Moves back one command in history |
| k | Moves forward one command in history |
| /string RETURN | Searches backward for command with *string* (not a regular exception except for ^ matching the start of the line) |
| ?string RETURN | Searches forward for command with *string* (see previous entry) |
| n | Repeats previous search |
| N | Repeats previous search in opposite direction |
| nv | Enters full-screen vi to edit command number *n*, or command if *n* is omitted |
| # | Inserts current command as a comment in history file |

# Miscellaneous Commands (vi)

| ESCAPE = | Lists pathnames that match current word (pathname listing) |
| ESCAPE \ | Completes current word to a unique or partial pathname (pathname completion) |
| ESCAPE * | Expands current word to all matching pathnames (pathname expansion) |
| U | Undoes previous change |
| ~ | Changes case of current character |
| n | Repeats, *n* times, the most recent command that caused a change; if *n* is omitted, it defaults to one |
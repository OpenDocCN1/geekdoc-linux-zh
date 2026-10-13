# Filename Substitution

After parameter substitution and command substitution are performed on the command line, the shell looks for the special characters `*`, `?`, and `[`. If they're not quoted, the shell searches the current directory, or another directory if preceded by a `/`, and substitutes the names of all files that match. If no match is found, the characters remain untouched.

Note that filenames beginning with a `.` must be explicitly matched (in other words, `echo *` won’t display your hidden files but `echo .*` will).

The filename substitution characters are summarized in Table A.6.

**Table A.6 — Filename Substitution Characters**

| Character(s) | Meaning |
|---|---|
| `?` | Matches any single character. |
| `*` | Matches zero or more characters. |
| `[chars]` | Matches any single character in `chars`; the format `C₁-C₂` can be used to match any character in the range `C₁` through `C₂`, inclusive (for example, `[A-Z]` matches any uppercase letter). |
| `[!chars]` | Matches any single character not in `chars`; a range of characters may be specified as above. |

# I/O Redirection

When scanning the command line, the shell looks for the special redirection characters `<` and `>`. If found, they are processed and removed (with any associated arguments) from the command line. Table A.7 summarizes the different types of I/O redirection that the shell supports.

**Table A.7 — I/O Redirection**

| Construct | Meaning |
|---|---|
| `< file` | Redirect standard input from `file`. |
| `> file` | Redirect standard output to `file`; `file` is created if it doesn’t exist and zeroed if it does. |
| `>\| file` | Redirect standard output to `file`; `file` is created if it doesn’t exist and zeroed if it does; the `noclobber` (`-C`) option to `set` is ignored. |
| `>> file` | Like `>`, except that output is appended to `file` if it already exists. |
| `<< word` | Redirect standard input from lines that follow up until a line containing just `word`; parameter substitution occurs on the lines, and back-quoted commands are executed if the backslash character is interpreted; if any character in `word` is quoted, none of this processing occurs and the lines are passed through unaltered; if `word` is preceded by a `-`, leading tabs on the lines are removed. |
| `<<& digit` | Standard input is redirected from the file associated with file descriptor `digit`. |
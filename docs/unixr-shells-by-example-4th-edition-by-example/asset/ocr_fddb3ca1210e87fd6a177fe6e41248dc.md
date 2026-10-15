# Appendix B • Comparison of the Shells

| Feature | Bourne | Bash | Korn |
|---|---|---|---|
| Metacharacters for Filename Expansion (continued): |  |  |  |
| `*` | `[A−Z]` (sh) | `[ ]` | `abc?z(19)1` |
| `?` matches zero or more characters in the set |  |  |  |
| `[...]` matches any one character in the set. Parentheses, the vertical bar, and braces represent an OR condition. |  |  |  |
| `[...]` matches zero or more characters in the set. |  |  |  |
| `?` matches any one character. |  |  |  |
| `@(pattern)` |  |  |  |
| `?(pattern)` |  |  |  |
| `*(pattern)` |  |  |  |
| `+(pattern)` |  |  |  |
| `!(pattern)` |  |  |  |
| `abc?z(19)1` |  |  |  |

| Feature | Bourne | Bash | Korn |
|---|---|---|---|
| **I/O Redirection and Pipes:** |  |  |  |
| Command output redirected to a file | `cmd > file` | `cmd > file` | `cmd > file` |
| Command output appended to a file | `cmd >> file` | `cmd >> file` | `cmd >> file` |
| Command input redirected from a file | `cmd < file` | `cmd < file` | `cmd < file` |
| Command errors redirected | `(cmd > /dev/tty) 2>errors` | `cmd 2> file` | `cmd 2> errors` |
| Output and errors redirected to a file | `cmd > file 2>&1` | `cmd &> file or cmd > file 2>&1` | `cmd > file 2>&1` |
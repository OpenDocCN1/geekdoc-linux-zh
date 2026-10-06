# Builtin (Continued)

| | |
|---|---|
| [] | The test command (see the chargs script on page 628) |
| [ ] | Similar to [ ] adds string comparisons (page 756) |

The Z Shell supports the redirection operators shown in (Table 15-3).

# Redirection Operators

| | |
|---|---|
| < filename | Redirects standard input from filename. |
| <> filename | Redirects standard input from standard output to filename. If NOCLOBER is unset (that is, if CLOBBER is set), this redirection creates filename if it does not exist. |
| > filename | Redirects standard output to filename. If NOCLOBER is unset (that is, if CLOBBER is set), this redirection creates filename if it does not exist. |
| >= filename or >! filename | Redirects standard output to filename, even if the file exists and the NOCLOBER option (page 825) is set (that is, if CLOBBER is not set). |
| >> filename | Redirects and appends standard output to filename. If NOCLOBER is unset (that is, if CLOBBER is set), this redirection creates filename if it does not exist. |
| <&n | Duplicates standard input from file descriptor n. |
| >&n | Duplicates standard output from file descriptor n. |
| [n]<&- | Closes standard input or file descriptor n if specified. |
| [n]&- | Closes standard output or file descriptor n if specified. |
| [n]<&p | Transfers the input from the coprocess (page 806) to standard input or file descriptor n if specified. |
| [n]>&p | Transfers the output to the coprocess (page 806) to standard output or file descriptor n if specified. |
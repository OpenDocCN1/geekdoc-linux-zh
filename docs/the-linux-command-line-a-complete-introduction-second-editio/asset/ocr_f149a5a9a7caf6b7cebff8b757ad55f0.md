# NOTE

Don’t worry if your results are not the same as this example. Every Linux distribution defines the prompt string a little differently, some quite exotically.

From the results, we can see that PS1 contains a few of the characters we see in our prompt such as the brackets, the at-sign, and the dollar sign, but the rest are a mystery. The astute among us will recognize these as backslash-escaped special characters like those we saw in Chapter 7. Table 13-1 provides a partial list of the characters that the bash treats specially in the prompt string.

# Table 13-1: Escape Codes Used in Shell Prompts

| Sequence | Value displayed |
|---|---|
| \a | ASCII bell. This makes the computer beep when it is encountered. |
| \d | Current date in day, month, date format. For example, “Mon May 26.” |
| \h | Hostname of the local machine minus the trailing domain name. |
| \H | Full hostname. |
| \j | Number of jobs running in the current shell session. |
| \l | Name of the current terminal device. |
| \n | A newline character. |
| \r | A carriage return. |
| \s | Name of the shell program. |
| \t | Current time in 24-hour hours:minutes:seconds format. |
| \T | Current time in 12-hour format. |
| \@ | Current time in 12-hour AM/PM format. |
| \A | Current time in 24-hour hours:minutes format. |
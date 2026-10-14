those we saw in Chapter 8. Here is a partial list of the characters that the shell treats specially in the prompt string:

# Table 14-1: Escape Codes Used In Shell Prompts

| Sequence | Value Displayed |
|---|---|
| \a | ASCII bell. This makes the computer beep when it is encountered. |
| \d | Current date in day, month, date format. For example, “Mon May 26.” |
| \h | Host name of the local machine minus the trailing domain name. |
| \H | Full host name. |
| \j | Number of jobs running in the current shell session. |
| \l | Name of the current terminal device. |
| \n | A newline character. |
| \r | A carriage return. |
| \s | Name of the shell program. |
| \t | Current time in 24 hour hours:minutes:seconds format. |
| \T | Current time in 12 hour format. |
| \@ | Current time in 12 hour AM/PM format. |
| \A | Current time in 24 hour hours:minutes format. |
| \u | User name of the current user. |
| \v | Version number of the shell. |
| \V | Version and release numbers of the shell. |
| \w | Name of the current working directory. |
| \W | Last part of the current working directory name. |
| \! | History number of the current command. |
| \# | Number of commands entered into this shell session. |
| \$ | This displays a “$” character unless you have superuser privileges. In that case, it displays a “#” instead. |
| \[ | Signals the start of a series of one or more non-printing characters. This is used to embed non-printing control characters which manipulate the terminal emulator in some way, such as moving the |
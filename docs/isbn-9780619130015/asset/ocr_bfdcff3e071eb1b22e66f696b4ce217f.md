# Customizing Your Prompt

Your login prompt is configured automatically when you login. An environment variable, PS1, contains special formatting characters that determine your prompt's configuration.

> **To see the contents of the PS1 environment variable:**

**1** Type `echo $PS1` and press **Enter**.

**2** You see the contents of the PS1 variable, which may appear as:
`[\u@\h \W]\$`

Characters that begin with \\ are special Bash shell formatting characters. \\u prints the user name, \\h prints the system host name, and \\W prints the name of the working directory. The \\$ character prints either a # or a $, depending on the type of user logged on. The brackets, [ and ], and the space that separates \\h and \\W, are not special characters, so they are printed just as they appear. When Jean is logged on to the system eli and working in her home directory, her prompt appears as [jean@eli jean]$ in the format shown above.

Table 2-1 shows other formatting characters for configuring your Bash shell prompt.

| **Formatting character** | **Purpose** |
| :--- | :--- |
| \\d | Displays the date |
| \\h | Displays the host name |
| \\n | Displays a new line |
| \\nnn | Displays the ASCII character that corresponds to the octal number *nnn*. |
| \\s | Displays the shell name |
| \\t | Displays the time |
| \\u | Displays the user name |
| \\w | Displays the path of the working directory |
| \\W | Displays the name of the working directory without any other path information |
| \\! | Displays the number of the current command in the command history |

Table 2-1: Formatting characters for configuring a Bash shell prompt
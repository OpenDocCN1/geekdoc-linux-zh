# Table 9-5  **bash** keyword variables (continued)

| Variable | Value |
|---|---|
| LANG | The locale category when that category is not specifically set using one of the *LC_* variables (page 368) |
| LC_ | A group of variables that specify locale categories including *LC_ALL, LC_COLLATE, LC_CTYPE, LC_MESSAGES*, and *LC_NUMERIC*; use the *locale* builtin (page 369) to display a more complete list including values |
| LINES | The height of the display used by **select** (page 1012) |
| MAIL | The pathname of the file that holds a user's mail (page 360) |
| MAILCHECK | How often, in seconds, **bash** checks for mail (default: 60; page 360) |
| MAILPATH | A colon-separated list of file pathnames that **bash** checks for mail in (page 360) |
| OLDPWD | The pathname of the previous working directory |
| PATH | A colon-separated list of directory pathnames that **bash** looks for commands in (page 359) |
| PROMPT_COMMAND | A command that **bash** executes just before it displays the primary prompt |
| PS1 | Prompt String 1; the primary prompt (page 361) |
| PS2 | Prompt String 2; the secondary prompt (page 362) |
| PS3 | The prompt issued by **select** (page 1012) |
| PS4 | The **bash** debugging symbol (page 995) |
| PWD | The pathname of the working directory |
| REPLY | Holds the line that *read* accepts (page 1042); also used by **select** (page 1012) |

# Special Characters

Table 9-6 lists most of the characters that are special to the **bash** shell.

# Table 9-6  Shell special characters

| Character | Use |
|---|---|
| NEWLINE | A control operator that initiates execution of a command (page 341) |
| ; | A control operator that separates commands (page 341) |
| ( ) | A control operator that groups commands (page 344) for execution by a subshell; these characters are also used to identify a function (page 396) |
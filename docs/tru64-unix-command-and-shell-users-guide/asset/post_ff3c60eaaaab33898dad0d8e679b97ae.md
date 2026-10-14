
## Table 8–4: C Shell Metacharacters (cont.)

| Metacharacter | Description |
|---|---|
| `~` | Specifies a home directory when used at the beginning of pathnames. |

### Quotation

| Metacharacter | Description |
|---|---|
| `'...'` | Specifies that any of the enclosed characters should be interpreted literally; that is, without their special meaning to the shell. |
| `"..."` | Provides a special form of quoting. Specifies that the `$` (dollar sign), `'` (grave accent), and `\` (backslash) characters keep their special meaning, while all other enclosed characters are interpreted literally; that is, without their special meaning to the shell. Double quotes are useful in making variable assignments. |

### Input/Output

| Metacharacter | Description |
|---|---|
| `<` | Redirects input. |
| `>` | Redirects output to a specified file. |
| `<<` | Redirects input and specifies that the shell should read input up to a specified line. |
| `>>` | Redirects output and specifies that the shell should add output to the end of a file. |
| `>&` | Redirects both diagnostic and standard output and appends them to a file. |
| `>>&` | Redirects both diagnostic and standard output to the end of an existing file. |
| `>!` | Redirects output and specifies that if the `noclobber` variable is set (prevents overwriting of files), it should be ignored so that the file can be overwritten. |

### Substitution

| Metacharacter | Description |
|---|---|
| `$` | Specifies variable substitution. |
| `!` | Specifies history substitution. |
| `^` | Precedes substitution modifiers. |
| `:̂` | Used in special kinds of history substitution. |
| `` ` `` | Specifies command substitution. |

## 8.2.3 Command History

The command history buffer stores the commands you enter and lets you display them at any time. As a result, you can select a previous command, or parts of previous commands, and then reexecute them. This feature may save you time because it lets you reuse long commands instead of reentering them.

You may want to enter the following three commands in your `.cshrc` file:

- `set history=n`

  Creates a history buffer that stores the command lines you enter. The *n* entry specifies the number of command lines you want to store in the history buffer.

- `set savehist=n`

  Saves the command lines you entered during the current login session and makes them available for the next login session. The *n* entry specifies the number of command lines you want to store in the history buffer when you log out.

- `set prompt=[\!]`

  Causes your C shell prompt to display the number of each command line.

To see the contents of the history buffer, use the `history` command. The displayed output will be similar to the following (your output will vary):

```
[18] % history
3 set history=15
4 pwd
5 cd /usr/sales
6 ls -l
7 cp report report5
8 mv /usr/accounts/new .
9 cd /usr/accounts/new
10 mkdir june
11 cd june
12 mv /usr/accounts/new/june .
13 ls -l
14 cd /usr/sales/Q1
15 vi earnings
16 cd /usr/chang
17 vi status
18 history
[19] %
```

To reexecute any command in the command history buffer, use the commands listed in Table 8-5. Each command starts with an exclamation point (!), which tells the C shell that you are using commands in the history buffer.

For example, assume that you often need to move to the directory /usr/chang/reports/status. You can create an alias status, which will move you to that directory whenever you enter it on the command line.

In addition, aliases let you make up more descriptive names for commands. For example, you could define an alias named rename for the mv command.

To create aliases, use the alias command. The format of the alias command is:

```
alias aliasname command
```

The aliasname entry specifies the name you want to use. The command entry specifies either the original command or a series of commands. If the command has more than one part (has spaces), enclose the whole expression in single quotes (' ').

For example, to create the alias status that moves you to the directory /usr/chang/reports/status, enter the following command:

```
% alias status 'cd /usr/chang/reports/status'
```

The usual way to define aliases is to make them a permanent part of your environment by including them in your .cshrc file. As a result, you can use the aliases whenever you log in or start a new shell. See Section 8.2.1 for an example.

To display all alias definitions, enter the following command:

```
% alias
```

To display the definition of a particular alias, enter the following command:

```
% alias aliasname
```

The aliasname entry specifies the particular alias for which you are requesting a definition.

To remove an alias for the current login session, use the unalias command. The general format of the unalias command is the following:

```
unalias aliasname
```

The aliasname entry specifies the alias you want to remove.

To remove an alias for the current and all future login sessions, do the following:

1. Enter the following command:
   % unalias aliasname
   The aliasname entry specifies the alias you want to remove.
2. Edit the .cshrc file and remove the alias definition. Then, save the file.
3. Enter the following command to reexecute the .cshrc file:

The backslash must be used to escape the normal use of the & command, which would just cause the command to be run in the background.

The HISTFILESIZE variable defines the number of entries of the history file. If the size is set to a value smaller than that of the current file, the file is truncated to the new value. The default setting is 500. The HISTSIZE variable specifies the size of the command history. Table 14-8 shows these variables.

Table 14-8 History Variables
| Variable | Function |
| HISTFILE | Holds the filename of the history file. |
| HISTCMD | Holds the history number of the current command. |
| HISTCONTROL | Defines which commands will not be added to the history list. The valid values are ignorespace, which ignores commands that start with a space; ignoredups, which ignores duplicate commands; and ignoreboth, which ignores both types of commands. |
| HISTIGNORE | Holds a colon-separated list of patterns that filters commands added to the history list. |
| HISTFILESIZE | Defines the number of entries that can be added to the history file. |
| HISTSIZE | Specifies the number of entries that are added to the resident history list. |

# Mail variables

The mail variables tell the shell where and how often to check for new mail so it can notify you. The shell just checks the defined files and determines if they have been modified since the last check.

The MAILCHECK variable controls how often the shell checks for new mail. The default is every 60 seconds. The MAIL variable holds the name of the mail file to check. This is usually the user's mail file in the spool directory.

```
debian:~$echo $MAIL
/var/spool/mail/root
```

The MAIL variable holds the location of only one mail file to check. Some mail programs use multiple mail files, or you may set up filters or rules to move where mail is stored. The MAILPATH variable holds a colon-separated list of filenames to check for new mail. For example:

```
MAILPATH=~/mail/work:~/mail/personal:~/mail/spam
```
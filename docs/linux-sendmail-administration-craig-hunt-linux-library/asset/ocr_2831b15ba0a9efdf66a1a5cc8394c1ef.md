Every recipe begins with :0, which differentiates it from an assignment statement. The :0 is optionally followed by flags that change how the filter is processed. Table 11.1 lists all of the flags and their use.

# Table 11.1 procmail Recipe Flags

| Flag | Meaning |
|---|---|
| A | Execute this recipe if the preceding recipe evaluates to true. |
| a | This has the same meaning as the A flag, except that the preceding recipe must also have successfully completed execution. |
| B | Pass the body of the message on the destination. This is the default. |
| B | Filter the message body. |
| c | Create a carbon copy of this mail. |
| D | Tests are case sensitive. By default case is ignored. |
| e | Execute this recipe if the execution of the preceding recipe returned an error. |
| E | Execute this recipe if the preceding recipe was not executed. |
| f | Pass the data through an external filter program. |
| H | Filter the message headers. This is the default. |
| h | Pass the message header to the destination. This is the default. |
| I | Ignore write errors for this recipe. |
| r | Write the mail out “as is” without ensuring it is properly formatted. |
| w | Check the exit code of the external filter program. |
| W | This is the same meaning as the w flag, except no error message is printed.

An optional lockfile can be identified to prevent multiple copies of procmail from writing to the same mailbox at the same time. This can happen on a busy system, causing some pretty strange-looking mail. The lockfile name is preceded by a colon:
# TABLE 17.1: SPECIAL CHARACTERS (CONTINUED)

| Character | Meaning |
| :--- | :--- |
| `<<` | Identifies here document |
| `*` | Identifies a string of characters in an ambiguous file reference |
| `?` | Identifies a single character in an ambiguous file reference |
| `\\` | Quotes the following character |
| `'` | Quotes a string; no substitutions allowed |
| `"` | Quotes a string; allows variable, command substitution |
| `...` | Performs command substitution |
| `[ ]` | Identifies a character class in an ambiguous file reference |
| `.` | Built-in; executes command or script in current shell instead of spawning a new shell |
| `\\` | Logical OR; executes command on right if command on left fails |
| `!` | Logical NOT; reverses exit status |

# TABLE 17.2: VARIABLES/PARAMETERS

| Variable | Purpose |
| :--- | :--- |
| `$0` | Gives the name of the script being called. However, in the shell, it would report the shell you are in. |
| `$n` | Gives the value of the nth command argument. |
| `$*` | Gives all command-line arguments. |
| `$#` | Gives a count of the command-line arguments. |
| `$$` | Gives the PID number of the current process. |
| `$!` | Gives the PID number of the most recent background task. |
| `$?` | Gives exit status of last task. |

# Local Variables

Basic conventions for assigning values to variables are the same in the Bourne and Korn shells. There is no white space in a variable; it should be one word as in the following example:

```
$ bvos=Imn
```
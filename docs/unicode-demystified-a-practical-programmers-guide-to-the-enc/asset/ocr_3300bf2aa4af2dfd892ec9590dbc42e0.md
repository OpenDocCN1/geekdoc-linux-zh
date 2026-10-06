# Special Symbols

# Display in Prompt (Continued)

| | |
|---|---|
| %M | The full hostname, including the domain |
| %n | Your login name |
| %t | The time of day through the current minute |
| %p | The time of day through the current second |
| %d | The day of the week |
| %D | The day of the month |
| %W | The month as mm |
| %y | The year as yy |
| %Y | The year as yyy |
| %# | A greater than sign (>) if you are not Superuser; a pound sign (#) if you are |
| %? | The result returned by the preceding command |

prompt2 Holds the prompt used in foreach and while control structures (pages 720 and 722). The default value is '%R? ', where the R is replaced by the word while if you are inside a while structure and foreach if you are inside a foreach structure.

prompt3 Holds the prompt used during automatic spelling correction. The default value is 'CORRECT>$R(y|n|e|a)', where the R is replaced by the corrected string.

savehist Specifies the number of commands saved from the history list when you log out. These events are saved in a file named .history in your home directory. The shell uses them as the initial history list when you log in again, causing your history list to continue across login sessions.

shell Holds the pathname of the shell you are using.

shl This variable increments each time you start a subshell and decrements each time you exit a subshell. The value is set to 1 for login shells.

status Contains the exit status returned by the last command.

tcsh Holds the version number of tcsh that you are running. See the version variable (page 711) for more detail.
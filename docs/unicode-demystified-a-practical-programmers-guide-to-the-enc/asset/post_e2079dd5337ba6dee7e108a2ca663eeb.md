
# Options (Continued)

Options marked with an asterisk (*) are set by default in a login shell.

- UNSET (+u) - Treats unset parameters as empty and does not generate an error as would be the case if this option were not set.
- VERBOSE (-v) Displays each input line as the shell reads.
- XTRACE (-x) Prints commands as they are executed. Does not print function calls or commands, such as (( and [.
- ZLE (-z) Enables the Z Shell line editor.*

# Chapter Summary

The Z Shell implements nearly all the features of the Bourne Again Shell, as well as the most useful features of the TC Shell. You can customize the Z Shell to create a personal interactive environment by choosing settings for options and values for variables and by defining aliases and functions.

You assign attributes to Z Shell variables with the typeset builtin. The Z Shell provides operators to perform pattern matching on variables, provide default values for variables, and evaluate the length of the value of variables. The Z Shell supports array variables and local variables for functions and built-in integer arithmetic capability, using the let builtin and an expression syntax similar to the C programming language.

Condition testing is similar to that of the test utility, the Z Shell provides more primitives, including string ordering and pattern matching. The Z Shell provides special syntax that uses arithmetic and logical expressions as conditions.

The Z Shell provides a rich set of control structures for conditions and iterative execution. The select control structure provides a simple method for creating menus in shell scripts and for repeatedly prompting the user for responses. The while, until, and if...then structures have the same syntax as their Bourne Shell counterparts but can take advantage of the Z Shell' more powerful logical and arithmetic condition testing. The repeat statement provides a convenient way to repeat a sequence of commands a number of times. Most Z Shell structures are also available with a TC Shell syntax for users who are more familiar with the TC Shell.

The Z Shell provides the ability to manipulate file descriptors. Coupled with powerful read and print builtins, this allows shell scripts to have much control over input and output as programs written in lower-level languages. The Z Shell provides all the I/O redirections of both bash and sh and more. A unique feature of the Z Shell is its ability to launch a coprocess: a process that executes in parallel with the parent shell whose standard input and output are connected via a two-way pipe to the parent shell. From the parent shell you can read standard output of the coprocess, using &. You can write to standard input of the coprocess, using &.

Functions are a powerful feature of the Z Shell. You can call them from an interactive Z Shell or from a script shell. Because they do not require a new process when they are called, Z Shell functions are more efficient than shell scripts. As functions in other modern programming languages, such as C, Z Shell functions may be recursive, which can lead to simpler solutions to some problems. The autoload built a function only if it is actually used, making functions more efficient and easier. The Z Shell also provides some functions that can be used to perform tasks periodically, to produce prompts that change dynamically, and to perform tasks when changing directories.

As with the Bourne Again Shell and the TC Shell, the Z Shell includes the ability to start jobs as background tasks, to suspend jobs in the foreground, and to move jobs between the background and foreground. Job control in the Z Shell closely matches that of the TC Shell than the Bourne Again Shell.

Shell and the rich set of builtins and control structures are well suited to the use of the Z Shell for both interactive and scripting purposes. The complete set of command line substitutions and expansions are particularly useful in interactive use.

When using an interactive Z Shell, you can edit your command line and commands from the history file, using either of the Z Shell's command line editors (vi or emacs). If you use the vi command editor, you start in Input mode, unlike the way you normally enter vi. You can switch between Command and Input mode. The emacs editor is mindless and distinguishes commands from editor input by recognizing control characters as commands.

# Commands for the vi Command Line Editor

Not all the available command line editor commands are given here. See the zsh command line editor (zshle) man page for a complete list.

# Cursor-Movement Commands (vi)

In addition to the following commands, you may be able to use the arrow keys to move about. The arrow keys work regardless of mode.

| I (lowercase "ell") | Moves one character to the right |
| h | Moves one character to the left |
| w | Moves one word to the right |
| b | Moves one word to the left |
| W | Moves one space-delimited word to the right |
| B | Moves one space-delimited word to the left |
| 0 | Moves to beginning of line |
| $ | Moves to end of line |
| e | Moves to end of word |
| E | Moves to end of space-delimited word |
| ^ | Moves to first nonblank position on line |
| fx | Moves to next (right) occurrence of x |
| Fx | Moves to previous (left) occurrence of x |
| ; (semicolon) | Repeats last t or F command |
| , (comma) | Repeats last t or F command but in opposite direction |
| nl | Moves to column n |

# Changing Text (vi)

| i | Enters Insert mode before current character |
| a | Enters Insert mode after current character |
| l | Enters Insert mode before first nonblank character |
| A | Enters Insert mode at end of line |
| rx | Replaces current character with x |
| R | Overwrites, starting at current character, until ESCAPE |
| nx | Deletes n characters, starting at current character |
| nX | Deletes n characters, starting just past current character |
| D | Deletes from current character to end of line |
| dd | Deletes entire command |
| C | Changes from current character to end of line |

# History Editing Commands (vi)

| j | Moves back one command in history |
| k | Moves forward one command in history |
| /string RETURN | Searches backward for command with *string* (not a regular exception except for ^ matching the start of the line) |
| ?string RETURN | Searches forward for command with *string* (see previous entry) |
| n | Repeats previous search |
| N | Repeats previous search in opposite direction |
| nv | Enters full-screen vi to edit command number *n*, or command if *n* is omitted |
| # | Inserts current command as a comment in history file |

# Miscellaneous Commands (vi)

| ESCAPE = | Lists pathnames that match current word |
| ESCAPE \ | Completes current word to a unique or partial pathname |
| ESCAPE * | Expands current word to all pathnames |
| U | Undoes previous change |
| ~ | Changes case of current character |
| n | Repeats, *n* times, the most recent command that caused a change; if *n* is omitted, it defaults to one |

# Commands for emacs Command Line Editor

Not all the emacs mode commands are given here. See the zsh command line editor (zshle) man page for a complete list.

# Cursor-Movement Commands (emacs)

In addition to the following commands, you may be able to use the ARROW keys to position the cursor.

| CONTROL-F | Moves one character to the right |
| CONTROL-B | Moves one character to the left |
| ESCAPE f | Moves one word to the right |
| ESCAPE b | Moves one word to the left |
| CONTROL-A | Moves to beginning of line |
| CONTROL-E | Moves to end of line |
| CONTROL-| x | Moves to next instance of x |

# Changing Text (emacs)

| Erase | Deletes character to the right of current character |
| CONTROL-D | Deletes current character |
| CONTROL-K | Deletes to end of line |
| Kill | Deletes entire line |
| CONTROL-T | Transposes current and previous (to left) characters |
| CONTROL-W | Deletes all characters from current character to Mark |
| ESCAPE D | Deletes one word to right |
| ESCAPE h | Deletes one word to left |
| ESCAPE l | Changes next word to all lowercase |
| ESCAPE C | Changes first letter of word to uppercase |

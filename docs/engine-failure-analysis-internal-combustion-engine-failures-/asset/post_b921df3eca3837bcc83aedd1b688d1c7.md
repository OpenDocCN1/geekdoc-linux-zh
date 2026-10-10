
## USING KEYBOARD MACROS

| Use This Keyboard Shortcut | To Do This |
|---------------------------|-------------|
| Ctrl + x e | Replay last keyboard macro |
| Ctrl + x { | Start a keyboard macro |
| Ctrl + x } | Stop a keyboard macro |

## EXECUTING COMMANDS

| Use This Keyboard Shortcut | To Do This |
|---------------------------|-------------|
| Ctrl + g | Cancel the command |
| Ctrl + l | Clear the screen |
| Return | Execute the command |
| Ctrl + j | |
| Ctrl + m | |

## Overview of Shell Command Syntax

You can enter most commands by typing the command's name, followed by a space and the options and arguments you want to use. To create more complex commands, you need to learn the fundamentals of bash's syntax, the rules that specify precisely how such commands are constructed:

**Special characters and quoting** Certain characters have a special meaning to bash. If you want to use these characters in a way other than how bash interprets them, you must enclose them in quotation marks. For example, you may wish to begin a filename with a hash mark (#). However, bash interprets this character to represent the beginning of a non-executing comment. If you wish to use the hash mark for a purpose other than beginning a comment, you must enclose the hash mark in quotation marks.

**Metacharacters** A *metacharacter* is a special character that functions as a *word separator*, as if it were a blank space. However, not all special characters are metacharacters. Some special characters will not serve their intended function unless you place a space before them.

## Command sequences and groups

You can type more than one command on a single line so that they are executed together in the specified sequence from left to right. To alter the default execution sequence, you can arrange commands in groups so that the commands enclosed by parentheses or brackets are executed first.

## Input/output redirection

By default, bash reads from the standard input (the keyboard) and writes output to the standard output (the display); or, in the case of an error, to the standard error (again, the display). With input/output redirection, you can redirect output to another command or to a file. You can also tell a command to take input from a file.

You should also understand how bash uses expansion, a method of generating a lengthier entry from a shorthand expression. To use expansion, you use special expansion characters. After you press Enter, bash reads (parses) your command; detects the expansion characters, and generates the lengthier command in accordance with your instructions. You can use the following types of expansion:

- **Brace expansion**: This shell capability enables you to generate several output patterns from a single entry.
- **Tilde expansion**: This shell capability gives you quick ways to enter directory names.
- **Command substitution**: This shell capability enables you to construct commands by inserting a command’s output. A common use of this capability is `$pwd`, a command substitution that inserts the output of the `pwd` command (see Chapter 2). This command’s output is the current directory.
- **History expansion**: The shell keeps track of the commands you have entered by creating a history list. By means of history expansion, you can re-use commands you previously entered.
- **Parameter expansion**: Parameters are named entities, such as variables. You can define your own variables and insert their values using parameter expansion. In addition, you can make use of a number of built-in variables.

**Shell functions** With *shell functions*, you can group two or more commands and assign them to a name of your choosing.

**Job control** You can use the shell to place lengthy processes in the background, as long as they can operate without intervention. An example of such a job is compiling a large program. Background programs have a *job ID* and can be brought back to the foreground or suspended by means of bash commands.

## Special Characters and Quoting

Some characters have special meaning for bash. If you wish to use them for purposes other than those indicated here, you must protect them with quotation characters. Note that some of these special characters are *metacharacters*, which separate words even if you omit spaces; however, other characters do not perform a word separation function. For example, parentheses are metacharacters, but curly braces are not. If you create a command using curly braces and fail to type a space before and after each curly brace, the command will not work.

**TIP** When quoting, it is safest to use single quotation marks rather than double quotation marks, unless you have a special reason to use double quotation marks. Double quotation marks preserve the special meaning of several characters, such as `*`, `$`, and `` ` ``.

The following tables detail information concerning special characters and quoting:

- The **Special Characters** table shows all the characters that have special meaning to bash.
- The **Quotation Characters** table shows the punctuation you can use to prevent bash from processing special characters.
- The **Metacharacters** table shows special characters that also function as word separators.

### SPECIAL CHARACTERS

| Special Character | Purpose |
| :--- | :--- |
| `` ` `` | Quotes all of the enclosed text, preventing all expansions or substitutions. |
| `!` | A logical NOT in a command sequence. |
| `"` | Quotes the enclosed text with the exception of variable expansion and command substitution. |
| `#` | Inserts a comment; bash ignores the rest of the line. |
| `$` | Inserts a named variable. It is also used for command and arithmetic substitution. |
| `&` | When appended to a command name, executes a command in the background. |
| `&&` | A logical AND in a command sequence. |
| `()` | Groups commands for execution by a subshell. It is also used to identify a function. |
| `*` | Stands for zero or any characters in a shell pattern. |
| `./` | When placed at the beginning of a line, executes a command in the working directory that is not on the current path. |
| `:` | A null command. |
| `?` | Stands for any one character in a shell pattern. |
| `[]` | Defines a character class in a shell pattern. |
| `\` | Quotes the following character. |
| `""` | Indicates a command substitution. |
| `{}` | Groups commands. These are also used for brace expansion. |
| `\|` | Redirects the command output to a second command. |
| `\|\|` | A logical OR in a command sequence. |
| `<` | Takes input from a file rather than from the keyboard. |
| `<<` | Uses the standard input but only up to the specified text. |
| `>` | Redirects the command output to a file. |
| `>>` | Appends the command output to a file. |
| `%` | Indicates a job number. |

### QUOTATION CHARACTERS

| Quotation Character | Purpose |
| :--- | :--- |
| `\` | This character is called the *escape character*. It preserves the literal meaning of the following character, except newline characters. |
| `' '` (single quotes) | Preserves the literal meaning of all characters within the single quotes. |
| `" "` (double quotes) | Preserves the literal meaning of all the characters within the quotes, with the exception of those that initiate variable expansion ($) and command substitution (). |

### METACHARACTERS

| Metacharacter | Purpose |
| :--- | :--- |
| `\|` | Pipeline |
| `&` | Command substitution |
| `;` | Command separator |
| `( )` | Command grouping for execution in a subshell |
| `< >` | Redirection operators |

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `cat 'income $ expenses.doc'` | Displays the text of `income $ expenses.doc`. If single quotes were not used, the shell would interpret the dollar sign ($) as a variable substitution. |
| `dir '$pwd/chapter (overview)'` | Specifies a directory to be displayed using command substitution ($pwd). The double quotation marks protect the parentheses from interpretation by the shell but enable the use of command substitution. |

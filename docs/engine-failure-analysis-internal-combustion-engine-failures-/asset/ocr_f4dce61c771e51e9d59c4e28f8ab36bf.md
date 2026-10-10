# Command sequences and groups

You can type more than one command on a single line so that they are executed together in the specified sequence from left to right. To alter the default execution sequence, you can arrange commands in groups so that the commands enclosed by parentheses or brackets are executed first.

# Input/output redirection

By default, bash reads from the standard input (the keyboard) and writes output to the standard output (the display); or, in the case of an error, to the standard error (again, the display). With input/output redirection, you can redirect output to another command or to a file. You can also tell a command to take input from a file.

You should also understand how bash uses expansion, a method of generating a lengthier entry from a shorthand expression. To use expansion, you use special expansion characters. After you press Enter, bash reads (parses) your command; detects the expansion characters, and generates the lengthier command in accordance with your instructions. You can use the following types of expansion:

+   - Brace expansion	This shell capability enables you to generate several output patterns from a single entry.

+   - Tilde expansion	This shell capability gives you quick ways to enter directory names.

+   - Command substitution	This shell capability enables you to construct commands by inserting a command’s output. A common use of this capability is $pwd, a command substitution that inserts the output of the pwd command (see Chapter 2). This command’s output is the current directory.

+   - History expansion	The shell keeps track of the commands you have entered by creating a history list. By means of history expansion, you can re-use commands you previously entered.

+   - Parameter expansion	Parameters are named entities, such as variables. You can define your own variables and insert their values using parameter expansion. In addition, you can make use of a number of built-in variables.
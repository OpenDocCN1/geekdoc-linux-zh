Note that each option is preceded by a hyphen.

Most commands allow you to specify multiple options. Thus, to prepare a reversed long listing of all files in the directory D ir, flagging directories and executable files, you could type

$ ls -a -l -r -F D ir (Return)

Or you could combine the options:

$ ls -alrF D ir (Return)

Incidentally, anything that follows the command name—including the options and file names—is generally referred to as an argument.

# 8.4
The Standard Input, Output, and Error

Whenever you run a UNIX command, the operating system opens up three standard channels for input and output:

+   - Standard input. The standard input (or stdin) is the place the program normally looks for input.

+   - Standard output. The standard output (or stdout) is where the program sends its output.

+   - Standard error. The standard error (or stderr) is used by the program to display error messages.

# 8.5
Redirection

Most of the time we use terms "standard input" and "standard output" as synonyms for the keyboard and terminal screen, respectively. However, the shell allows you to redirect the standard output so that output goes into a file instead. For example, you have already seen how to use the output redirection operator (>) to create a file containing a calendar:

$ cal 1999 > calendar.file (Return)

You can add output to a file using the append operator (>>):

$ cal 2000 >> calendar.file (Return)

It is also possible to redirect the standard input so that a process takes its input from a file rather than the keyboard. For example, the mail command allows you to send and read electronic mail. To send the contents of the file my.message to the user jones, you could enter the command line

$ mail jones < my.message (Return)
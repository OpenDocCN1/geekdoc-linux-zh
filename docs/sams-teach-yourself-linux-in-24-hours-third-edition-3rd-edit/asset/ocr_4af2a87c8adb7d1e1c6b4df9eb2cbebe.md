+   - The bash shell includes a trait that allows you to type a portion of a command or filename and the shell will guess at the complete command or filename. You need to type enough of the command or filename so that it can be uniquely identified. After you type a few characters, press Tab and the shell completes the rest of the command. If the shell cannot make a guess, you will hear a beep and a list of potential commands appears. Enter more characters and try to complete the command again.
+   - One way to get more mileage out of a command is with the use of wildcard characters. Wildcards are used to select files or directories that meet certain requirements. The * wildcard replaces one or more characters in the file or directory name. The ? wildcard replaces a single character in the file or directory name. You'll work with wildcards in Hour 7, when you learn how to view the list of files in a directory.

![](bbox=[0.18, 0.53, 0.26, 0.64])

> Wildcards are used only for filenames and directory names. Do not use wildcards for command names or command options; Linux will not recognize the command.

# Changing the Standard Output

When you execute a command, the command is read from the keyboard (the standard input) and the results (or the output) of the command appear on the screen (the standard output). If you want the command output to appear in a different place, or if you want to send the output to another command for processing, you will need to change the output with a process called input/output redirection. Command redirection is done by separating two or more commands with the > or | character.

One way to redirect the output is to save the results of the command to a file instead of displaying it on the screen. This enables you to save a picture of the output for later use. The > character is used when you want to send the output of a command to a file or to a printer.

Most Linux commands are simple tools that perform a single task. There might be times when you need to combine two or more commands to do a job. For example, if the list of files that displays as the result of the ls command is too long to read, combine the ls command with the less pager. This gives you the ability to scroll through the file list.
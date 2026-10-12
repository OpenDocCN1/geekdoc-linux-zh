Some of the basic built-in commands have already been covered, such as alias, jobs, fg, and history. Here are some others that are also available:

+   - bindkey—Allows you to change the actions that are associated with key bindings.
+   - builtins—Prints out the names of all built-in commands.
+   - pwd—Prints out your present working directory.
+   - exec—Executes the specified command in place of the current shell.
+   - nice—Sets the scheduling for the shell to a number. The higher the number, the less cpu the process gets.
+   - printenv—Prints the names and values for all environment variables, or if a specific variable name is passed to it, it will only print information on that variable.
+   - eval—Evaluates any argument that is passed to it and displays the result.
+   - logout—Logs you out from the current shell.
+   - umask—The user file-creation mask is set to MODE. If MODE is omitted, or if -S is supplied, the current value of the mask is printed. The -S option makes the output symbolic; otherwise an octal number is output. If MODE begins with a digit, it is interpreted as an octal number, otherwise it is a symbolic mode string like that accepted by chmod.
+   - exit—Exits the shell with a status of N. If N is omitted, the exit status is that of the last command executed.
+   - set—Allows you to set the value for a shell variable.
+   - unset—Removes a variable.
+   - cd—Changes your present working directory to the directory you pass as an argument.
+   - source—Reads in the contents of any files passed to the command, and executes those contents.
+   - bg—Puts any jobs passed to it into the background, continuing any jobs that are stopped. You can pass a number of a string when referring to jobs.
+   - fg—Puts the job passed to it in the foreground.
+   - where—Prints out all known information about any command that is passed to it, including aliases, built-in commands, and executables in the path.
EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `gunzip ballistic.tar.gz; tar -xvf ballistic.tar` | Compresses ballistic.tar.gz and extracts the files from the archive. |
| `find readme.txt && cat readme.txt` | Displays readme.txt only if the **find** command succeeds (see Chapter 4). |
| `find readme.bak \|\| cp readme.txt readme.bak` | Makes a backup of readme.txt only if the **find** command fails (see Chapter 4). |

# Input/Output Redirection

With input/output redirection, you can redirect output from the standard output (the display) to a file. You can write a new file or append the output to an existing file. You can also tell a command to accept input from a file rather than from the standard input (the keyboard).

COMMAND FORMS

| Command Form | Meaning |
| :--- | :--- |
| `command1 \| command2` | Pipe output from command1 to command2. |
| `command > filename` | Direct output from command to the file specified by filename. |
| `filename < command` | Use filename as the input for command. |
| `command >> filename` | Append output from command to the file specified by filename; create the file, if necessary. |
| `command <> filename` | Use filename as both the input and the output for command. |
| `command >! filename` | Direct output from command to the file specified by filename, and overwrite the file if it exists. |
| `command << text` | Use the standard input for command, but only up to the specified text. |
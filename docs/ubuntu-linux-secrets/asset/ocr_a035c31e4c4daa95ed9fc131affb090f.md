# Using Multiple Commands

In Chapter 19, "The Ubuntu Command Line," you saw how to use the command-line interface (CLI) prompt of the shell to enter commands and view the command results. The key to shell scripts is the ability to enter multiple commands and process the results from each command, possibly even passing the results of one command to another. The shell allows you to chain commands together into a single step.

If you want to run two commands together, you can enter them on the same prompt line, separated with a semicolon:

```
$ date ; who
Mon Nov 03 19:44:35 EST 2008
rich :0 2008-11-03 18:23 (console)
rich pts/1 2008-11-03 18:24
rich pts/0 2008-11-03 18:42
barbara pts/2 2008-11-03 19:30
katie pts/3 2008-11-03 19:39
$
```

Congratulations, you just wrote a shell script! This simple script uses just two shell commands. The date command runs first, displaying the current date and time, followed by the output of the who command, showing who is currently logged on to the system. Using this technique you can string together as many commands as you wish, up to the maximum command-line character count of 255 characters.

Though using this technique is fine for small scripts, it has a major drawback: you have to enter the entire command on the command prompt every time you want to run it. Instead of having to manually enter the commands onto a command line, you can combine the commands into a simple text file. When you need to run the commands, just simply run the text file.

# Creating a Script File

To place shell commands in a text file, first you'll need to use a text editor (see Chapter 6, "Working With Text") to create a file, then enter the commands into the file.

When creating a shell script file, you must specify the shell you are using in the first line of the file. The format for this is:
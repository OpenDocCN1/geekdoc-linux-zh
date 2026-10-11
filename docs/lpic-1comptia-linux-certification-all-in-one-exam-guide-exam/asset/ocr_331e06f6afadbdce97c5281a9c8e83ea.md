Shell scripts can be edited with any text editor. They can be executed in one of two ways:

+   - Entering `/bin/bash script_filename`.
+   - Adding the execute permission to the script file using the `chmod` utility and entering the filename of the script at the shell prompt.

In addition, you can also add the path to the shell file to your `PATH` environment variable so users won't have to remember the full path to the file to use it. Alternatively, you can also move the script file to a directory that is already in the users' `PATH` environment variable, such as `/bin`.

In addition to running commands from a script, you can also read input from the user and assign it to a variable using the `read variable_name` command in a script. Script variables don't need to be declared if you are going to read text into them. However, if you want to read numbers into a variable that will be actually treated as numbers (so that you can perform arithmetic functions, for example), then you need to declare them first using the `declare -i variable_name` command in the script.

You can also use control structures in your scripts. Control structures allow you to configure your scripts so that they branch or loop based on conditions that you supply. To make a script that branches in two directions, you can use an `if/then/else` structure in your script. If the condition you specify in the structure is true, then one set of commands (under `then`) is executed. If the condition is false, then the commands under the `else` portion of the structure are executed. The syntax for using `if/then/else` structures in a script is as follows:

```
```
if condition then
    commands
else
    commands
fi
```
```

You can use the `test` command in an `if/then/else` structure to test a condition. You can use the following options with `test`:

+   - `-d`  Checks to see if the specified directory exists.
+   - `-e`  Checks to see if the specified file exists.
+   - `-f`  Checks to see if the specified file exists and if it is a regular file.
+   - `-G`  Checks to see if the specified file exists and is owned by a specified group.
+   - `-h` or `-L`  Checks to see if the specified file exists and if it is a symbolic link.
+   - `-O`  Checks to see if the specified file exists and if it is owned by the specified user ID.
+   - `-r`  Checks to see if the specified file exists and if the read permission is granted.
+   - `-w`  Checks to see if the specified file exists and if the write permission is granted.
+   - `-x`  Checks to see if the specified file exists and if the execute permission is granted.
```
echo "The file exists and you can write to it."
else
# echo "You cannot write to the file."
#
fi
$
$ ls -l $HOME/newFile
ls: cannot access `/home/christine/newFile': No such file or directory
$
$ ./AndBoolean.sh
You cannot write to the file.
$
$ touch $HOME/newFile
$
$ ./AndBoolean.sh
The file exists and you can write to it.
```

Using the AND Boolean operator, both of the comparisons must be met. The first comparison checks to see if the `$HOME` directory exists for the user. The second comparison checks to see if there's a file called `newFile` in the user's `$HOME` directory and if the user has write permissions for the file. If either of these comparisons fails, the `if` statement fails, and the shell executes the `else` section. If both of the comparisons succeed, the `if` statement succeeds, and the shell executes the `then` section.

# Working with Advanced if-then Features

Three additions to the Bash shell provide advanced features that you can use in `if`-then statements:

+   •	Single parentheses for running the command in a subshell
+   •	Double parentheses for mathematical expressions
+   •	Double square brackets for advanced string handling functions

The following sections describe each of these features in more detail.

# Using single parentheses

Single parentheses allow you to use subshells in your `if` statement comparisons. Subshells were covered in Chapter 5, “Understanding the Shell.” This is the format of the single parentheses `test` command:

```
(_command_)
```

Before the Bash shell executes `command`, it creates a subshell in which to run the command. If the command completes its task successfully, the exit status (covered in Chapter 11) is set to 0, and the commands listed under the `then` section are executed. If the exit status of the command is anything else, the `then` commands aren't executed. Here's a script to test using subshells:
Do you see how this program saved us some work? Rather than having to go through each month manually, we were able to use a loop that increments a variable and automates the task of getting the value for each month. If we had used separate variables to store the temperatures, this task would have required a good deal more code than we used here.

> NOTE  
> If you want some good practice, see if you can modify the previous temperature program to use a `for` loop instead of a `while` loop. Here is a hint: Remember that the array can accept the asterisk wildcard to show all the elements in the array.

# Command Substitution

The Korn shell also supports a cleaner form of command substitution than the Bourne shell. Rather than putting commands in backquotes, you can use a syntax like the following:

```
today_date=$(date)
```

The old style is also still supported. Which one you use in Korn shell scripts is mostly a matter of personal preference.

# Using getopt

The `getopts` command offers a better way of handling command-line arguments than the simple Bourne-style syntax used earlier in the chapter. It allows you to use the standard option syntax of -option that most other FreeBSD commands use. It also allows for better handling of arguments to the options.

The general syntax of the `getopts` command looks like this:

```
getopts options variable
```

Here, *options* is the list of valid options that can be supplied, and *variable* is the name of the variable in which those options should be stored. If an option letter ends with a colon, it can also take a value. That value will be stored in the special variable `$OPTARG`. Another special variable, named `$OPTIND`, stores the value of the current argument being worked on.

The `getopt` command executes once for each option that is supplied with. If used with the `while` loop, the loop will execute once for each command-line argument supplied. The following shows an example of how the `getopt` command syntax works:

```
getopts abc:d: MyVar
```
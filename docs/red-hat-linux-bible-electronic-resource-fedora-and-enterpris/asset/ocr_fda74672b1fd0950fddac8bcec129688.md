files except for those that include the string xyzzy. Finally, the vi command opens all filenames for editing (one at a time) that include xyzzy.

This particular example may be useful if you knew that you wanted to edit a file for which you knew the name but not the location. As long as the string was uncommon, you could find and open every instance of a filename existing beneath a point you choose in the file system.

# Expanding arithmetic expressions

There may be times when you want to pass arithmetic results to a command. There are two forms you can use to expand an arithmetic expression and pass it to the shell: $[expression] or $((expression)). Here is an example:

```
$ echo "I am $[2003 - 1957] years old."
I am 46 years old.
```

In this example, the shell interprets the arithmetic expression first (2003 - 1957), and then passes that information to the echo command. The echo command displays the text, with the results of the arithmetic (46) inserted.

# Expanding variables

Environment variables that store information within the shell can be expanded using the dollar sign ($) metacharacter. When you expand an environment variable on a command line, the value of the variable is printed instead of the variable name itself, as follows:

```
$ ls -l $BASH
-rwxr-xr-x 1 root root 625516 Dec 5 11:13 /bin/bash
```

Using $BASH as an argument to ls -1 causes a long listing of the bash command to be printed. For more information on shell environment variables, see the following section.

# Using shell environment variables

Every active shell stores pieces of information that it needs to use in what are called environment variables. An environment variable can store things such as locations of configuration files, mailboxes, and path directories. They can also store values for your shell prompts, the size of your history list, and type of operating system.

To see the environment variables currently assigned to your shell, type the declare command. (It will probably fill more than one screen, so type declare | more.) You can refer to the value of any of those variables by preceding it with a dollar sign ($) and placing it anywhere on a command line. For example:

```
$ echo $USER
chris
```
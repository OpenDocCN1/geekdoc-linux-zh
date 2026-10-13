Here list is executed in a separate shell (called a sub-shell) and any changes the commands in list make to the working directory (via calls to cd) or environment variables will not affect the values in the script that invoked list.

As an example, the following function allows you to determine the absolute pathname of a directory without altering your current working directory:

```
abspath () { cd "$1" && pwd ; }
```

# Variable and Argument Questions

This section examines some questions that relate to variables and their use in shell scripts. It also covers questions related to command-line arguments.

# How can I include functions and variable definitions located in one script in to another script?

To include functions and variable definitions defined in one script in to another script, you need to use the . command as follows:

```
. file
```

Here file is the pathname of the script you want to include. This topic is covered in detail in Chapter 21, "Problem Solving with Functions."

![](bbox=[0.18, 0.85, 0.25, 0.92])

> When you include a file using the . command, make sure that the file does not contain the exit command as this will cause the current instance of the shell to exit.
> If you are using the . command to include a file in your login session, your session will be terminated and you will have to log in again.

# Is it possible to consider each argument to a shell script one at a time?

This can be accomplished using a for loop of the following form:

```
for arg in "$*"
do
  list
done
```
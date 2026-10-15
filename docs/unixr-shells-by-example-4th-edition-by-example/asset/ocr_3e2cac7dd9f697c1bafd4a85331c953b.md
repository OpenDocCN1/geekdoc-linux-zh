# EXPLANATION

The name of the function is dir. The empty parentheses are necessary syntax for naming the function but have no other purpose. The commands within the curly braces will be executed when dir is typed. The purpose of the function is to list only the subdirectories below the present working directory. The spaces surrounding the curly braces are required.

# 8.7.1 Unsetting Functions

To remove a function from memory, the unset command is used.

# FORMAT

```
unset function_name
```

# 8.7.2 Function Arguments and the Return Value

Because the function is executed within the current shell, the variables will be known to both the function and the shell. Any changes made to your environment in the function will also be made to the shell. Arguments can be passed to functions by using positional parameters. The positional parameters are private to the function; that is, arguments to the function will not affect any positional parameters used outside the function.

The return command can be used to exit the function and return control to the program at the place where the function was invoked. (Remember, if you use exit anywhere in your script, including within a function, the script terminates.) The return value of a function is really just the value of the exit status of the last command in the script, unless you give a specific argument to the return command. If a value is assigned to the return command, that value is stored in the $? variable and can hold an integer value between 0 and 255. Because the return command is limited to returning only an integer between 0 and 255, you can use command substitution to capture the output of a function. Place the entire function in backquotes and assign the output to a variable just as you would if getting the output of a UNIX command.

# EXAMPLE 8.48

```
(Using the return command)
(The Script)
#!/bin/sh
# Scriptname: do_increment
1 increment () {
2   sum= `expr $1 + 1`
3   return $sum   # Return the value of sum to the script.
}
```